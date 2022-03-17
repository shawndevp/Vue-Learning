<template>
<div id="app">
  <UserProfile/>
</div>
</template>

<script>
import UserProfile from "./components/UserProfile.vue";

export default {
  name: 'App',
  components: { UserProfile }
}

</script>

<style>
@import './assets/base.css';

#app {
  /* max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal; */
  font-family: Avenir, Helvetica, Arial, sans-serif;
  --webkit-font-smoothing: antialiasied;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
}
/* 
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
} */
</style>
