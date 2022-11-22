<script setup>
  // import VideoPlayer.vue
  import VideoPlayer from './components/VideoPlayer.vue'
  // import VideoDetails.vue
  import VideoDetails from './components/VideoDetails.vue'
  // import VideoComments.vue
  import VideoComments from './components/VideoComments.vue'

</script>

<template>
  <div class="app">
    <div class="videoPlayer"><VideoPlayer /></div>
    <div class="videoDetails"><VideoDetails /></div>
    <div class="videoComments"><VideoComments /></div>
  </div>
</template>

<style scoped>
  .app {  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  gap: 0px 0px;
  grid-auto-flow: row;
  grid-template-areas:
    "videoPlayer videoPlayer videoDetails"
    "videoPlayer videoPlayer videoComments"
    "videoPlayer videoPlayer videoComments";
}

.videoPlayer { grid-area: videoPlayer; }

.videoDetails { grid-area: videoDetails; }

.videoComments { grid-area: videoComments; }


</style>
