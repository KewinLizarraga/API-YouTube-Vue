<template>
  <div>
    <!-- <a :href="'https://www.youtube.com/watch?v='+video.id.videoId" target="_blank">
      <img class="card-img-left" :src="video.snippet.thumbnails.medium.url" alt="miniatura YouTube" />
    </a>-->
    <div class="card-body">
      <h5 class="card-title">
        <a
          :href="'https://www.youtube.com/watch?v=' + video.id.videoId"
          class="card-link"
          target="_blank"
        >{{ video.snippet.title }}</a>
      </h5>
      <!-- <h5 class="card-title">{{video.snippet.title}}</h5> -->
      <h6
        class="card-subtitle"
      >{{video.snippet.channelTitle}} | {{video.snippet.publishedAt || formatDate}}</h6>
      <p class="card-text mb-2 text-muted">{{video.snippet.description}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "VideoList",
  props: ["video"]
};
</script>