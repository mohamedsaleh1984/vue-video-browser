<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="videos"/>
    <!--
      <VideoList v-bind:videos="videos"/>
      <VideoList :videos="videos"/>
    -->
    {{videos.length}}
  </div>
 
</template>
<script>
import SearchBar from './components/SearchBar.vue'
import VideoList from './components/VideoList.vue'
/**/
import axios from 'axios'
const API_KEY ='AIzaSyCn1wKF5XAP4rjNN_vAarfCb3HmabBWfCI'


export default {
  name: 'app',
  components: {
    SearchBar,
    VideoList
  },
  data: function() {
    return {
      videos:[]
    }
  },
  methods: {
    onTermChange: function(searchTerm) {
        //console.log(searchTerm);
        /**/
        axios.get('https://www.googleapis.com/youtube/v3/search',{
          params:{
            key:API_KEY,
            type:'video',
            part:'snippet',
            q: searchTerm
          }
       }).then(response => {this.videos = response.data.items;});
       
    }
  }
}
</script>
