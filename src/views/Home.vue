<template>
  <v-layout row wrap class="pa-6">
    <v-flex v-for="movie in movies" xs4 class="pa-5" :key = "movie._id">
      <v-card>
        <v-card-title primary-title>
          <div>
            <div class="headline">
              <v-btn flat v-bind:to="`/movies/${movie._id}`">
                {{movie.name}}
              </v-btn>
            </div>
            <span class="grey-text">{{movie.release_year}}, {{movie.genre}}</span>
          </div>          
        </v-card-title>
        <v-card-text>
         {{movie.description}}
        </v-card-text>
      </v-card>
    </v-flex> 
  </v-layout>
</template>

<script>
import axios from 'axios';

export default {
  name : 'Movies',
  data(){
    return {
      movies:[]
    };
  },
  mounted(){
   this.fetchMovies();
  },
  methods:{
    async fetchMovies(){
      return axios({
        method:'get',
        url:'http://localhost:8081/api/movies'
      })
      .then(res =>{
        this.movies = res.data.movies ;
      })
      .catch(err =>{
        return err ;
      })
    }
  }  
}
</script>


