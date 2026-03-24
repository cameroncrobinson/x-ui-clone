<template>
  <div class="tweet">
    <div class="tweet-inner">
      <img :src="tweet.profilePic" class="profile-pic">
      <div>
        <p class="handle">{{ tweet.handle }}</p>
        <p class="tweet-text">{{ tweet.tweetText }}</p>
        <div class="tweet-details">
          <span class="tweet-detail">
            <i class="fa-regular fa-comment-dots" @click="toggleReplies"></i>
            {{ tweet.replies.length }}
          </span>
          <span class="tweet-detail">
            <i :class="['fa-solid fa-heart', { liked: tweet.isLiked }]" @click="$emit('like', tweet.uuid)"></i>
            {{ tweet.likes }}
          </span>
          <span class="tweet-detail">
            <i :class="['fa-solid fa-retweet', { retweeted: tweet.isRetweeted }]" @click="$emit('retweet', tweet.uuid)"></i>
            {{ tweet.retweets }}
          </span>
        </div>
      </div>
    </div>
    <div v-if="tweet.replies.length > 0" :class="{ hidden: !showReplies }" :id="`replies-${tweet.uuid}`">
      <div v-for="reply in tweet.replies" :key="reply.uuid" class="tweet-reply">
        <div class="tweet-inner">
          <img :src="reply.profilePic" class="profile-pic">
          <div>
            <p class="handle">{{ reply.handle }}</p>
            <p class="tweet-text">{{ reply.tweetText }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tweet',
  props: {
    tweet: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showReplies: false
    };
  },
  methods: {
    toggleReplies() {
      this.showReplies = !this.showReplies;
    }
  }
};
</script>

<style scoped>
/* Component styles */
</style>