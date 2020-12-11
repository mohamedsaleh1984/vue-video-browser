<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail v-bind:video="selectedVideo"></VideoDetail>
      <VideoList @videoSelect="onVideoSelect" :videos="videos" />
    </div>

    <!--
      <VideoList v-bind:videos="videos"/>
      <VideoList :videos="videos"/>
    -->
    <div>Total number of videos :: {{ videos.length }}</div>
  </div>
</template>
<script>
import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";
import VideoDetail from "./components/VideoDetails.vue";
/**/
import axios from "axios";
const API_KEY = "AIzaSyCn1wKF5XAP4rjNN_vAarfCb3HmabBWfCI";

export default {
  name: "app",
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return {
      videos: [],
      selectedVideo: null,
    };
  },
  methods: {
    onVideoSelect: function (video) {
      this.selectedVideo = video;
      console.log("Video Selected Updated.");
    },
    onTermChange: function (searchTerm) {
      console.log(searchTerm);
      /**/
      /**/
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        })
        .then((response) => {
          this.videos = response.data.items;
        });
    },
  },
};
</script>
