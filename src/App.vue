<template>

    <div class="container">
      <!-- emit 2. 듣고, -->
      <SearchBar @input-change="onInputChange"/>
      <div class="row">
        <VideoDetail :video="selectedVideo"/>
        <VideoList @video-select="onVideoSelect" :videos="videos"/> 
      </div>
    </div>

</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

import SearchBar from './components/SearchBar.vue'
import VideoList from './components/VideoList.vue'
import VideoDetail from './components/VideoDetail.vue'

//현재는 이렇게 처리하지만 나중에는 바꿔야 한다! 보안적인 이슈가 크다
const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      inputValue: '',
      videos: [],
      selectedVideo: null, //스르륵하고 올라온 데이터를 잡는 것이다.
    }
  },
  methods: {
    onInputChange(inputText) {
      this.inputValue = inputText,
      axios.get(API_URL, {
        params: {
          key: API_KEY,
          part: 'snippet', //꼭 써야 한다.
          type: 'video', // 설정으로  channel1, playlist, video를 넣을 수 있다.
          q: this.inputValue,
        }
      })
        .then(res => {
          res.data.items.forEach(item => {
          const parser = new DOMParser()
          const doc = parser.parseFromString(item.snippet.title, 'text/html')
          item.snippet.title = doc.body.innerText
          })
          this.videos = res.data.items
        })
        .catch(err => console.error(err))
    },
    onVideoSelect(video) {
      console.log('3: App: 받았다!', video)
      this.selectedVideo = video 
    }
  }
}
</script>

<style>

</style>
