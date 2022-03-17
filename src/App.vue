
<template>

<div id="app">
  @{{user.username}} - {{fullName}}
  <strong>Followers:</strong> {{followers}}
  <button v-on:click="followUser">
    Follow
  </button>
</div>

</template>

<script>

  export default {
    name: 'App',
    data() {
      return {
        followers: 0,
        user: {
          id: 1,
          username: '_Tjadam',
          firstName: 'Shawn',
          lastName: 'Orn',
          email: 'Shawn@test.com',
          isAdmin: true
        }
      }
    },
    watch: {
      followers(newFollowerCount, oldFollowerCount) {
        if(oldFollowerCount < newFollowerCount) {
          console.log(`${this.user.username} has gained a follower!!`)
        }
      }
    },
    computed: {
      fullName() {
        return `${this.user.firstName} ${this.user.lastName}`;
      }
    },
    methods: {
      followUser() {
        this.followers++;
      }
    },
    mounted() {
      this.followUser();
    }
  }

</script>

<style>
@import './assets/base.css';

#app {
  /* max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal; */
  display: flex;
  flex-direction: column;
  text-align: center;
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
