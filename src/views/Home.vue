<template>
  <div class="home">
    <FilterNav
      @filterChange="currentFilter = $event"
      :currentFilter="currentFilter"
    />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
import FilterNav from '../components/FileNav'

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data () {
    return {
      projects: [],
      currentFilter: 'all',
    }
  },
  mounted () {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.error(err))
  },
  computed: {
    filteredProjects () {
      if (this.currentFilter === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      else if (this.currentFilter === 'onGoing') {
        return this.projects.filter(project => !project.complete)
      }
      else {
        return this.projects
      }
    }
  },
  methods: {
    handleDelete (id) {
      this.projects = this.projects.filter(project => project.id !== id)
    },
    handleComplete (id) {
      const tempProject = this.projects.find(project => project.id === id)
      tempProject.complete = !tempProject.complete
    }
  }
}
</script>
