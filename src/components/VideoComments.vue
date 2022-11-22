<script setup>

import { ref, reactive, onMounted } from 'vue';

  let comments = reactive({ comments : [] });
  let text = ref("");

  onMounted(() => {
    // fetch API
    fetch("https://lab5-p379.onrender.com/api/v1/messages/")
      .then((response) => response.json())
      .then((data) => {
        comments.comments = data;
        console.log(data);
      });
  });

  const addComment = () => {
    let data = {
      user: "Liam",
      text: text.value
    };
    fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    })
      .then((response) => response.json())
      .then((data) => {
        console.log("werkt?");
        comments.comments.push({
          _id: data.data._id,
          user: data.data.user,
          text: data.data.text,
        });
      });
  };

  




</script>

<template>
  <div>
    <div  >
        <ul class="comments">
            <li v-for="comment in comments.comments" :key="comment.id">
                <div class="comment">
                    <h3>{{comment.user}}</h3>
                    <p>{{comment.text}}</p>
                </div>
            </li>
        </ul>

        <div class="commentInput">
            <input type="text" placeholder="Type comment" v-model="text" />
            <button @click="addComment">Add comment</button>
        </div>
        
    </div>
  </div>
</template>

<style scoped>

.comments{
    width: 100;
    height: 500px;
    overflow: scroll;
}

</style>
