<template>
  <section class="section">
    <div class="initial">
      <h1 class="title">TuitCombinator</h1>
      <span :class="['field', {'is-pulled-right': width > 512}]">
        <input id="configTheme"
               type="checkbox"
               name="configTheme"
               class="switch is-rounded is-outlined"
               @click="toggleDarkTheme">
        <label for="configTheme">
          <font-awesome-icon class="icon" icon="moon" />
        </label>
      </span>
    </div>
    <div class="columns">
      <div class="column box">
        <FeedColumn :feed="makeschool"></FeedColumn>
      </div>
      <div class="column box">
        <FeedColumn :feed="newsycombinator"></FeedColumn>
      </div>
      <div class="column box">
        <FeedColumn :feed="ycombinator"></FeedColumn>
      </div>
    </div>
  </section>
</template>

<script>
import FeedColumn from './components/Feed.vue'
import makeschool from './components/makeschool.json'
import newsycombinator from './components/newsycombinator.json'
import ycombinator from './components/ycombinator.json'

export default {
  name: 'app',
  components: {
    FeedColumn
  },
  data() {
    return {
      width: window.innerWidth,
      makeschool,
      newsycombinator,
      ycombinator
    }
  },
  methods: {
    toggleDarkTheme() {
      let body = document.body
      if (body.classList) {
        body.classList.toggle('dark')
      } else {
        let classes = el.className.split(' ')
        let existingIndex = classes.indexOf('dark')
        if (existingIndex >= 0) {
          classes.splice(existingIndex, 1)
        } else {
          classes.push('dark')
        }
        el.className = classes.join(' ')
      }
    }
  }
}
</script>

<style lang="scss">
.columns {
  margin-top: 1.2rem;
  align-items: flex-start;
  flex-wrap: wrap;
}
.dark {
  background-color: #263238;
  color: #EDEFEF;
  strong {
    color: white;
    font-weight: bold;
  }
  & .box, & .title {
    background-color: #263238;
    color: #EDEFEF !important;
  }
  & .box {
    border: 1px solid #ACACAD;
  }
  & .tweet-link, & .subtitle {
    color: #EDEFEF;
    a, a:link, a:visited {
      color: #03C6AB;
    }
  }
}
.title, .field {
  display: inline-block;
}
</style>
