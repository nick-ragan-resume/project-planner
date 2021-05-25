<template>
  <!-- bind class complete if project.compete is true -->
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: {id: project.id} }">
            <span class="material-icons">edit</span>
        </router-link>
        <!-- Add click event to delete icon -->
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="toggleComplete" class="material-icons tick">done</span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      // add data so we don't have to type the endpoint several times
      // we need the projects id to select the correct project
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    // Create a method for click event attached to icon
    deleteProject() {
      // fetch endpoint and pass in a delete method
      fetch(this.uri, { method: "DELETE" })
        // fires callback once this.uri is deleted
        // create custom event to emit that we will call delete
        // send the project id along with the custom event
        .then(() => this.$emit("delete", this.project.id))
        // catch any errors that may occur
        .catch((err) => console.log(err));
    },

    toggleComplete() {
      // Patch request - to update a certain part of an item - when you don't want to update the whole item
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }),
      }).then(() => this.$emit("complete", this.project.id))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #6b6b6b;
  max-width: 600px;
  border-bottom: 5px solid rgba(22, 22, 22, 0.1);
  border-right: 5px solid rgba(22, 22, 22, 0.1);
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
/* if project is complete add this border color */
.complete {
  border-left: 4px solid #00ce89;
}
/*If project is complete add color to tick*/
.project.complete .tick {
  color: #00ce89;
}
</style>