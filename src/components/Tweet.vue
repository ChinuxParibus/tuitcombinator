<template>
<div class="box">
  <a class="tweet-link" :href="info.tweet_link" target="_blank">
    <div class="media">
      <div class="media-content">
        <div class="content">
          <p>
            <strong>{{ info.tweet_date }}</strong>
            <br>
            <span v-html="info.tweet_text"></span>
          </p>
        </div>
      </div>
    </div>
  </a>
</div>
</template>

<script>
export default {
  name: 'TweetCard',
  props: {
    tweet: Object
  },
  computed: {
    info: {
      get() {
        let self = this
        let lookupText = self.tweet.full_text
        let RElinks = /([--:\w?@%&+~#=]*\.[a-z]{2,4}\/{0,2})((?:[?&](?:\w+)=(?:\w+))+|[--:\w?@%&+~#=]+)?/gi
        let REmentions = /@\w+/gi
        let mapDays = {
          'Sun': 'Sunday',
          'Mon': 'Monday',
          'Tue': 'Tuesday',
          'Wed': 'Wednesday',
          'Thu': 'Thursday',
          'Fri': 'Friday',
          'Sat': 'Saturday'
        }
        let mapMonths = {
          'Jan': 'January',
          'Feb': 'February',
          'Mar': 'March',
          'Apr': 'April',
          'May': 'May',
          'Jun': 'June',
          'Jul': 'July',
          'Aug': 'August',
          'Sep': 'September',
          'Oct': 'October',
          'Nov': 'November',
          'Dec': 'December'
        }
        let content = {
          tweet_link: `https://twitter.com/${self.tweet.user.screen_name}/status/${self.tweet.id_str}`,
          tweet_date: '',
          tweet_text: lookupText.includes('RT')
            ? `${lookupText.slice(0, lookupText.indexOf(':'))}: ${self.tweet.retweeted_status.full_text}`
            : lookupText
        }

        content['tweet_date'] = self.tweet.created_at.split(' ')
        content['tweet_date'][3] = [content['tweet_date'][5], content['tweet_date'][5] = content['tweet_date'][3]][0]
        content['tweet_date'].pop(4)
        content['tweet_date'] = `${mapDays[content['tweet_date'][0]]},
          ${mapMonths[content['tweet_date'][1]]} ${content['tweet_date'][2]},
          ${content['tweet_date'][3]}`

        content['tweet_text'] = content['tweet_text']
          .replace(RElinks, '<a href="$&" target="_blank">$&</a>')
          .replace(REmentions, '<a href="https://twitter.com/$&" target="_blank">$&</a>')

        return content
      },
      set(v) {}
    }
  }
}
</script>

<style lang="scss">
.tweet-link {
  color: #263238;
}
</style>
