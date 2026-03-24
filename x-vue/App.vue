<template>
  <div id="app">
    <header>
      <h1>Twonk</h1>
    </header>
    <main>
      <div class="tweet-input-area">
        <img src="https://fastly.picsum.photos/id/419/200/300.jpg?hmac=jvSs1zyCZ3ATdTlvdfcTKBBGcrgnCk3EAvZt352Fbco" class="profile-pic">
        <textarea v-model="tweetText" placeholder="What's happening?"></textarea>
      </div>
      <button @click="addTweet">Tweet</button>
      <div class="feed">
        <Tweet v-for="tweet in tweets" :key="tweet.uuid" :tweet="tweet" @like="handleLike" @retweet="handleRetweet" />
      </div>
    </main>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'https://jspm.dev/uuid';
import { tweetsData } from '../js/data.js';
import Tweet from './Tweet.vue';

export default {
  name: 'App',
  components: {
    Tweet
  },
  data() {
    return {
      tweets: tweetsData,
      tweetText: ''
    };
  },
  methods: {
    handleLike(tweetId) {
      const tweet = this.tweets.find(t => t.uuid === tweetId);
      if (tweet.isLiked) {
        tweet.likes--;
      } else {
        tweet.likes++;
      }
      tweet.isLiked = !tweet.isLiked;
    },
    handleRetweet(tweetId) {
      const tweet = this.tweets.find(t => t.uuid === tweetId);
      if (tweet.isRetweeted) {
        tweet.retweets--;
      } else {
        tweet.retweets++;
      }
      tweet.isRetweeted = !tweet.isRetweeted;
    },
    addTweet() {
      if (this.tweetText.trim()) {
        const newTweet = {
          handle: '@Scrimba',
          profilePic: 'images/scrimbalogo.png',
          likes: 0,
          retweets: 0,
          tweetText: this.tweetText,
          replies: [],
          isLiked: false,
          isRetweeted: false,
          uuid: uuidv4(),
        };
        this.tweets.unshift(newTweet);
        this.tweetText = '';
      }
    }
  }
};
</script>

<style>
/* Add styles here or import */
</style>