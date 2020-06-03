<template>
  <li @click="onVideoSelect" class="video-list-item list-group-item">
    <img :src="thumbnailUrl" class="mr-3" alt="youtube-thumbnail-image">
    <div class="media-body">
      {{ video.snippet.title }}
    </div>
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    video: Object,
  },
  methods: {
    // 비디오가 선택되었으면, 비디오가 선택되었다는 'video-selected'를 부모에게 방출한다.
    onVideoSelect() {
      //console.log("1: Video List Item Selected!")
      this.$emit('video-select', this.video) //video-select 말과 함께 video를 상위 컴포넌트로 보낸다.
    }
  },
  computed: {
    // 함수지만 이름은 명사형. 왜? 결국 리턴되는 값으로 사용되기 때문이다.
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url
    }
  }
}
</script>

<style scoped>
  li.video-list-item{
    display:flex;
    cursor: pointer;
  }
  li.video-list-item:hover {
    background-color: #eee;
  }

  .media-body {
    margin: auto 0
  }

</style>