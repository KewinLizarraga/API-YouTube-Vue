<template>
  <div id="app">
    <Header />
    <SearchForm @search="search" />
    <SearchResult
      v-if="videos.length > 0"
      :videos="videos"
      :reformattedSearchString="reformattedSearchString"
    />
    <Pagination
      v-if="videos.length > 0"
      :prevPageToken="api.prevPageToken"
      :nextPageToken="api.nextPageToken"
      @prev-page="prevPage"
      @next-page="nextPage"
    />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/layout/Header";
import SearchForm from "./components/SearchForm";
import SearchResult from "./components/SearchResults";
import Pagination from "./components/Pagination";

export default {
  name: "app",
  components: {
    Header,
    SearchForm,
    SearchResult,
    Pagination
  },
  data() {
    return {
      videos: [],
      reformattedSearchString: "",
      api: {
        // Sobre la API --> https://developers.google.com/youtube/v3/docs/search/list
        baseUrl: "https://www.googleapis.com/youtube/v3/search?",
        part: "snippet", // (id, snippet)
        type: "video", // (channel, playlist, video)
        order: "viewCount", // (date, rating, relevance, title, videoCount, viewCount)
        maxResults: 12, // (0 - 50, default 5)
        q: "", // El parámetro q especifica el término de consulta que se debe buscar.
        key: YOUR_API_KEY,
        prevPageToken: "", // Token que se puede utilizar como valor del parámetro pageToken para recuperar la página anterior en el conjunto de resultados.
        nextPageToken: "" // Token que se puede utilizar como valor del parámetro pageToken para recuperar la página siguiente en el conjunto de resultados.
      }
    };
  },
  methods: {
    search(searchParams) {
      this.reformattedSearchString = searchParams.join(" ");
      this.api.q = searchParams.join("+");
      const { baseUrl, part, type, order, maxResults, q, key } = this.api;
      const apiUrl = `${baseUrl}part=${part}&type=${type}&order=${order}&maxResults=${maxResults}&q=${q}&key=${key}`;
      this.getData(apiUrl);
    },
    prevPage() {
      const {
        baseUrl,
        part,
        type,
        order,
        maxResults,
        q,
        key,
        prevPageToken
      } = this.api;
      const apiUrl = `${baseUrl}part=${part}&type=${type}&order=${order}&maxResults=${maxResults}&q=${q}&key=${key}&pageToken=${prevPageToken}`;
      this.getData(apiUrl);
    },
    nextPage() {
      const {
        baseUrl,
        part,
        type,
        order,
        maxResults,
        q,
        key,
        nextPageToken
      } = this.api;
      const apiUrl = `${baseUrl}part=${part}&type=${type}&order=${order}&maxResults=${maxResults}&q=${q}&key=${key}&pageToken=${nextPageToken}`;
      this.getData(apiUrl);
    },
    getData(apiUrl) {
      axios
        .get(apiUrl)
        .then(res => {
          this.videos = res.data.items;
          this.api.prevPageToken = res.data.prevPageToken;
          this.api.nextPageToken = res.data.nextPageToken;
          console.log(this.videos);
          console.log(apiUrl);
          
          
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>