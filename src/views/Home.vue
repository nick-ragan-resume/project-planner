<template>
  <div class="home">
    <!--Check length of projects -->
    <div v-if="projects.length">
      <!-- Loop through projects. Make the project.id the key -->
      <div v-for="project in projects" :key="project.id">
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

export default {
  name: "Home",
  // tell vue the components used on this page
  components: {
    SingleProject,
  },
  // return projects data
  data() {
    return {
      projects: [],
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
    },
  },
};
</script>

<style>
</style>