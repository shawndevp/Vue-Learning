
<template>

<div class="user-profile">
    <div class="user-profile__user-panel">
        <h1 class="user-profile__username">  @{{user.username}}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">
            Verified
            </div>
                   <div class="user-profile__admin-badge" v-else>
            Not verified
            </div>
            <div class="user-profile__follower-count">
                <strong>Followers:</strong> {{followers}}
            </div>
    </div>
  <!-- <button v-on:click="followUser">
    Follow
  </button> -->
  <div class="user-profile__tweets-wrapper">
      <!-- <div class="user-profile__tweet" v-for="tweets in user.tweets" :key="tweets.id">
          {{ tweets.content }}
      </div> -->
      <TweetItem v-for="tweet in user.tweets" :key="tweet.id" :username="user.username" :tweet="tweet" />
  </div>
</div>
</template>

<script>
import TweetItem from "./TweetItem.vue";

  export default {
    name: 'UserProfile',
    components: { TweetItem },
    data() {
      return {
        followers: 0,
        user: {
          id: 1,
          username: '_Tjadam',
          firstName: 'Shawn',
          lastName: 'Orn',
          email: 'Shawn@test.com',
          isAdmin: true,
          tweets: [
              {id:1, content: 'Twitter is awesome :)'},
              {id:2, content: 'Twitter number twooo :)'}
          ]
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


<style scoped>

.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    widows: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
    background: rebeccapurple;
    color: #fff;
    border-radius: 5px;
    margin: auto;
    padding: 0 10px;
    font-weight: bold;
}

h1 {
    margin: 0;
}

</style>