<template>
  <div class="header-container">
    <h1 >Project Task List</h1>
  </div>
  <div class="home">
    <div class="filters">
      <!-- pass filterChange from FilterNav as event and set it equal to the argument passed through -->
      <!-- send prop called current to FilterNav and set it equal to the current data value -->
      <FilterNav @filterChange="current=$event" :current="current" />
    </div>
    <!--Check length of projects -->
    <div v-if="projects.length">
      <!-- Loop through projects. Make the project.id the key -->
      <div v-for="project in filterProjects" :key="project.id">
        <!-- Use component created in the components directory -->
        <!-- Click event listens for event emitted from component callback -->
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
// import component
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";

export default {
  name: "Home",
  // tell vue the components used on this page
  components: {
    SingleProject,
    FilterNav
  },
  // return projects data
  data() {
    return {
      projects: [],
      // default event value
      current: 'all'
    };
  },
  mounted() {
    // fetch data from uri
    fetch("http://localhost:3000/projects")
      // jsonify data from uri
      .then((res) => res.json())
      // set projects array equal to data
      .then((data) => (this.projects = data))
      // catch any errors that occure during the above processes
      .catch((err) =>
        console.log(err.message, " ...this was the error message")
      );
  },
  methods: {
    // method called after delete emit callback triggers it
    // project.id passed as arguement
    handleDelete(id) {
      // return boolean if true the projects array will filter out project with id sent from emit callback
      // if false then a project id in projects array matches id sent from emit callback
      // so we would want to keep it in
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    handleComplete(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.complete = !p.complete;
    }
  },
  computed: {
    filterProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
};
</script>

<style>
h1 {
  text-align: center;
  margin: 50px 0 50px 0;
}

</style>