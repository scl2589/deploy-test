<template>
    <!--<ul>
      <li v-for="video in videos" :key="video.etag">
        {{ video.snippet.description }}
      </li>
    </ul> -->
    <!-- 이렇게 컴포넌트에도 v-for를 쓸 수 있다.
    :video="video" 이렇게 바인드를 걸어야 v-for에서 꺼내고 있는 video를 활용한다.-->
    <!--VideoListItem에 있는 onVideoSelect와 중첩된다고 해서 아무런 연관이없다 -->
    <ul class="list-group col-lg-4">
      <VideoListItem 
      @video-select="onVideoSelect"
      :video="video" 
      v-for="video in videos" 
      :key="video.etag"/>
    </ul> 
  
</template>

<script>
// function onVideoSelect(event) {
//   console.log(event.target)
// }
// button.addEventListener('video-select', onVideoSelect)

import VideoListItem from './VideoListItem.vue'

export default {
  name: 'VideoList',
  components: {
    VideoListItem,
  },
  props: {
    videos: Array, //videos라는 일므으로 배열이 넘어올거야
  },
  methods: {
    // 이름이 동일해도 어차피 VideoListItem component와 분리되어 있기 떄문에 상관 없음.
    onVideoSelect(video) {
      //console.log('2: Video List: Video Selected!', video.snippet.title)
      this.$emit('video-select', video)
    }
  }
} 
</script>

<style>

</style>