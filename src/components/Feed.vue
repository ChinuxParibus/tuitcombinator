<template>
  <div>
    <h2 class="subtitle" v-html="account"></h2>
    <TweetCard v-for="_tweet in feed" :tweet="_tweet" :key="_tweet.id"></TweetCard>
  </div>
</template>

<script>
import TweetCard from './Tweet.vue'

export default {
  name: 'FeedColumn',
  components: {
    TweetCard
  },
  props: {
    feed: Array
  },
  computed: {
    account() {
      return `Tweets from: <a href="https://twitter.com/@${this.feed[0].user.screen_name}"
      target="_blank">@${this.feed[0].user.screen_name}</a>`
    }
  }
}
</script>

<style lang="scss">
.column {
  margin-left: 2px;
  margin-right: 2px;
}
</style>
