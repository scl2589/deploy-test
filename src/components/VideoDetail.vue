<template>
  <div v-if="video" class="col-lg-8">
    <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item"
        :src="videoUrl" 
        allowfullscreen></iframe>
      </div>
    <div class="details">
      <!-- innerHTML
      <h4 v-html="video.snippet.title"></h4> -->
      <!-- innerText -->
      <h4 v-text="video.snippet.title"></h4>
      <p> {{ video.snippet.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    video: Object, //selectedVideo가 내려올건데, 이는 Object 형식일거야
  },
  // Read만 하되, 조작은 하고 값이 나갈 때 computed를 사용한다.
  computed: {
    videoUrl() {
      return `https://www.youtube.com/embed/${this.video.id.videoId}`
    }
  }
}
</script>

<style scoped>
  div.details {
    margin-top: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }

</style>