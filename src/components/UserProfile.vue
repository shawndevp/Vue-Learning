<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Verified</div>
      <div class="user-profile__admin-badge" v-else>Not verified</div>
      <div class="user-profile__follower-count">
        <strong>Followers:</strong> {{ followers }}
      </div>
      <form class="user-profile__create_tweet" @submit.prevent="createNewTweet">
        <label for="newTweet"><strong>New Tweet</strong></label>
        <textarea id="newTweet" rows="4" v-model="newTweetContent" />

        <div class="user-profile__create-tweet-type">
          <label for="newTweetType"><strong>Type: </strong></label>
          <select id="newTweetType" v-model="selectedTweetType">
            <option
              :value="option.value"
              v-for="(option, index) in tweetTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button>Send Tweet!</button>
      </form>
    </div>
    <!-- <button v-on:click="followUser">
    Follow
  </button> -->
    <div class="user-profile__tweets-wrapper">
      <!-- <div class="user-profile__tweet" v-for="tweets in user.tweets" :key="tweets.id">
          {{ tweets.content }}
      </div> -->
      <TweetItem
        v-for="tweet in user.tweets"
        :key="tweet.id"
        :username="user.username"
        :tweet="tweet"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem.vue";

export default {
  name: "UserProfile",
  components: { TweetItem },
  data() {
    return {
      newTweetContent: "",
      selectedTweetType: "instant",
      tweetTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Tweet" },
      ],
      followers: 0,
      user: {
        id: 1,
        username: "_Tjadam",
        firstName: "Shawn",
        lastName: "Orn",
        email: "Shawn@test.com",
        isAdmin: true,
        tweets: [
          { id: 1, content: "Twitter is awesome :)" },
          { id: 2, content: "Twitter number twooo :)" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log(`Favorite Tweet #${id}`);
    },
    createNewTweet() {
      if (this.newTweetContent && this.selectedTweetType !== "draft") {
        this.user.tweets.unshift({
          id: this.user.tweets.length + 1,
          content: this.newTweetContent,
        });
        this.newTweetContent = "";
      }
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style lang="scss" scoped>


.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  widows: 100%;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    h1 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background: rebeccapurple;
      color: #fff;
      border-radius: 5px;
      margin: auto;
      padding: 0 10px;
      font-weight: bold;
      margin-bottom: 20px;
    }

    .user-profile__create_tweet {
      border-top: 1px solid #dfe3e8;
      padding-top: 20px;
      display: flex;
      flex-direction: column;
    }
  }
  .user-profile__tweets-wrapper {
    display: grid;
    grid-gap: 10px;
  }
}
</style>
