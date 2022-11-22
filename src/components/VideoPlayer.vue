<script setup>
import { ref, reactive, onMounted } from 'vue';
import 'animate.css';

let src = ref('');
let videos = reactive({ videos : [] });
let animation = ref("");


 onMounted(() => {
   // fetch API
   let api_url = "http://127.0.0.1:5173/tiktok.json";
    fetch(api_url)
      .then((response) => response.json())
      .then((data) => {
        src.value = data.videos[0].video;
        videos.videos = data.videos;
      });

 });

 const nextVideo = () => {

    animation.value = "animate__fadeOut";
    setTimeout(() => {
      videos.videos.shift();
      src.value = videos.videos[0].video;
      animation.value = "animate__fadeIn";
    }, 1000);
    };






 // import ref
 /*import { ref, reactive } from 'vue';


 let title = ref("hello");
 let videos = reactive(["video1", "video2", "video3"]);

 const addVideo = () => {
   videos.push(title.value);
   console.log("werkt et?");
 };*/


</script>

<template>
    <div class="video">
        <div class="controls">
            <a @click.prevent="nextVideo" href="#" class="controls__next">⬇️</a>

        </div>
    <video :class="animation" class="animate__animated " :src="src" controls autoplay muted>
    </video>
    </div>

 <!-- <div>
    <h1>{{ title }}</h1>

    <ul>
      <li v-for="video in videos" :key="video">
        {{ video }}
      </li>
    </ul>

    <input type="text" v-model="title">
    <button @click="addVideo">Add video</button>
  </div>-->
</template>

<style scoped>

.video{
    position: relative;
}

.controls{
    position: absolute;
    right: 0;
    top:0;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.controls__next{
    font-size: 2rem;
    color: white;
    text-decoration: none;
    margin: 1rem;
}

video{
    max-width: 100%;
    max-height: 100%;
}

</style>
