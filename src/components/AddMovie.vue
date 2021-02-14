<template>
   <v-form v-model="valid" ref="form" lazy-validation>
       <v-text-field
       label="Movie Name"
       :rules="nameRules"
       v-model="name"
       required 
       >
       </v-text-field>
       <v-text-field
       label="Movie Description"
       name = "input-7-1"
       v-model="description"
       multi-line
       ></v-text-field>
       <v-select
          v-model="release_year"
          :items="years"
          label="Movie Release Year"
          :rules="releaseRules"
          required
        ></v-select>
       
       <v-text-field
       label="Movie Genre"
       v-model="genre"
       :rules="genreRules"
       required
       >
       </v-text-field>
       <v-btn
      @click="submit"
      :disabled="!valid"
    >
      submit
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
   </v-form>
</template>
<script>
import axios from 'axios';
export default {
    data: ()=>({
       valid:true,
       name:'',
       description:'',
       genre:'',
       release_year:'',
       nameRules:[
           v => !! v || 'Movie name is required',
       ]  ,
       releaseRules:[
           v => !!v || 'Realese year is required'
       ],
       genreRules:[
           v =>!!v || 'Movie genre is required',
           v => (v && v.length <= 80) || 'Movie genre is required between 80 characters'
       ],
       select:null,
       years:[
           '2018',
           '2017',
           '2016',
           '2015'
       ],
    }),
    methods:{
        submit(){
            
                //Perform Next Action
                return axios({
                    method:'post',
                    data:{
                        name:this.name,
                        description:this.description,
                        release_year: this.release_year,
                        genre:this.genre
                    },
                    url:'http://localhost:8081/movies/add',
                    headers:{
                        'Content-Type':'application/json',
                    },
                })
                .then((res)=>{
                    this.$swal(
                        'Great',
                        'Successfully Submited !',
                        'success'
                    )
                    this.$router.push({name:"Home"});
                    this.$refs.form.reset();
                })
                .catch((err)=>{
                    this.$swal(
                        'Oh ooppss!',
                        'Some goes wrong, Try again',
                        'error'
                    )
                   
                })
            
            return true;
        },
        clear(){
            this.$refs.form.reset();
        },
    },
};
</script>