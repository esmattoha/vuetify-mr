<template>
   <v-form v-model="valid" ref="form" lazy-validation>
       <v-text-field
       label="Username"
       :rules="nameRules"
       v-model="username"
       required 
       >
       </v-text-field>
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
       
       <v-text-field
       name = "input-7-1"
       label="Confirm Password"
       v-model="confirmpassword"
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

export default{
    data: ()=>({
        username:'',
        email:'',
        password:'',
        confirmpassword:'',

        emailRule:[
            v => !!v || "Email is required ",
            v => /\S+@\S+/.test(v) || "Email must be valid",
        ],
    }),
    methods:{
        async submit(){
            if(this.$refs.form.validate()){
                
            }
        },
        clear(){
            this.$refs.form.reset();
        }
    }
}
</script>
