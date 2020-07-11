<template>
  <div id="app" class="mainContainer">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/add/0">New Task</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}



.mainContainer{
    max-width: 600px;
    margin: auto;
    border: 3px solid #73AD21;
    background-color: lightgray;
}



</style>
