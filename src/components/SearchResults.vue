<template>
  <div class="container mb-3">
    <div class="d-flex mb-3">
      <div class="mr-auto">
        <h3>Resultado de busqueda para "{{ reformattedSearchString }}"</h3>
      </div>
      <div class="btn-group ml-auto" role="group">
        <button
          type="button"
          class="btn btn-outline-secondary"
          @click="changeDisplayMode('grid')"
          v-bind:class="{active: displayMode === 'grid'}"
        >
          <i class="fas fa-th"></i>
        </button>
        <button
          type="button"
          class="btn btn-outline-secondary"
          @click="changeDisplayMode('list')"
          v-bind:class="{active: displayMode === 'list'}"
        >
          <i class="fas fa-list"></i>
        </button>
      </div>
    </div>

    <div class="card-columns" v-if="displayMode === 'grid'">
      <div class="card" :key="video.id.videoId" v-for="video in videos">
        <VideoGridItem :video="video" />
      </div>
    </div>
    <div v-else>
      <div class="card mb-2" :key="video.id.videoId" v-for="video in videos">
        <VideoListItem :video="video" />
      </div>
    </div>
  </div>
</template>

<script>
import VideoGridItem from "./VideoGridItem";
import VideoListItem from "./VideoListItem";

export default {
  name: "SearchResults",
  components: {
    VideoGridItem,
    VideoListItem
  },
  data() {
    return {
      title: "Resultados de busqueda",
      displayMode: "grid"
    };
  },
  methods: {
    changeDisplayMode(displayMode) {
      this.displayMode = displayMode;
    }
  },
  props: ["videos", "reformattedSearchString"]
};
</script>

<style scoped>
button:focus {
  box-shadow: none !important;
}
</style>