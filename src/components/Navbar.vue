<template>
  <nav class="main-nav">
      <router-link :to="{ name: 'Home' }">Projects</router-link> |
      <router-link :to="{ name: 'AddProject'}">Add New Project</router-link>
  </nav>
</template>

<script>

</script>

<style>
  .main-nav {
    text-align: center;
    margin: 0 auto;
    padding-top: 20px;
    padding-bottom: 20px;
    background-color: rgb(32, 32, 32);
    width: 100%;
  }
  .main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: rgb(221, 221, 221);
    font-size: 18px;
  }
  a.router-link-active {
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
  }
</style>