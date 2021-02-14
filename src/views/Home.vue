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
import { application } from 'express';
import { json } from 'body-parser';

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
      const token = window.localStorage.getItem('auth');
      return axios({
        method:'get',
        url:'http://localhost:8081/movies',
        headers:{
          authorization: `JWT ${token}`,
         ' Content-Type': 'application/json'
        }
      })
      .then(res =>{
        this.movies = res.data.movies ;
        this.current_user = res.data.current_user;
      })
      .catch(err =>{
        return err ;
      })
    }
  }  
}
</script>


