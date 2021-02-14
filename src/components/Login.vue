<template>
   <v-form v-model="valid" ref="form" lazy-validation>
      
       <v-text-field
       label="Email"
       v-model="email"
       :rules="emailRule"
       required
       ></v-text-field>
       <v-text-field
          v-model="password"
          label="Password"
          required
        ></v-text-field>
       
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
export default{
    data: ()=>({
        email:'',
        password:'',

        emailRule:[
            v => !!v || "Email is required ",
            v => /\S+@\S+/.test(v) || "Email must be valid",
        ],
    }),
    methods:{
        async submit(){
            if(this.$refs.form.validate()){
                return axios({
                    method:'POST',
                    data:{
                        email: this.email,
                        password: this.password
                    },
                    url:'/user/register',
                    headers:{
                        'Content-Type':'application/json',
                    },
                })
                 .then((responce)=>{
                     window.localStorage.setItem('auth', responce.data.token);
                    this.$swal(
                        'Great',
                        'You have been successfully Login!',
                        'success'
                    )
                    this.$router.push({name:"Home"});
                   
                })
                .catch((error)=>{
                    const message = error.responce.data.message;
                    this.$swal(
                        'Oh ooppss!',
                       `${message}`,
                        'error'
                    )
                });
            }
            return true;
        },
        clear(){
            this.$refs.form.reset();
        }
    }
}
</script>
