<template>
  <div>
    <div class="card-body">
      <div class="row">
        <div class="col-3">
          <img class="card-img-top" :src="video.snippet.thumbnails.medium.url" alt="miniatura YouTube" />
        </div>
        <div class="col-9">
          <h5 class="card-title">
            <a
              :href="'https://www.youtube.com/watch?v=' + video.id.videoId"
              class="card-link"
              target="_blank"
            >{{ video.snippet.title }}</a>
          </h5>
          <h6
            class="card-subtitle"
          >{{video.snippet.channelTitle}} | {{video.snippet.publishedAt | formatDate}}</h6>
          <p class="card-text mb-2 text-muted">{{video.snippet.description}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "VideoList",
  props: ["video"]
};
</script>