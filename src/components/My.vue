<template>
  <div>
   
     <br> <input type="text" placeholder="EMAIL" v-model="email">
     <br> <input type="text" placeholder=" NAME " v-model="name">
     <br> <input type="text" placeholder="PAssword" v-model="password">
     <br> <button @click="checkfileds"> Submit </button>
   
    <div v-for="error of v$.email.$errors" :key="error.$uid">
      {{error.$message}}
    </div>
    <div v-for="error of v$.password.$errors" :key="error.$uid">
      {{error.$message}}
    </div>
    <div v-for="error of v$.name.$errors" :key="error.$uid">
      {{error.$message}}
    </div>
  </div>
</template>

<script>
import useValidate from '@vuelidate/core'
import { required,email } from '@vuelidate/validators'
export default {
    name:'My',
    data()
    {
        return{
          v$:useValidate(),
          email:'',
          name:'',
          password:'',
        }
    },
    validations(){
        return{
          email:{required,email},
          name:{required},
          password:{required},
        }
    },
    methods:{
      checkfileds(){
        this.v$.$validate()
        if(!this.v$.$error)
        {
          // alert("ERROR");
        }
        else
        {
          // alert("DONE ");
        }
        console.log(this.v$);
        // alert("CLICK")
      }
    }

}
</script>

<style>
    
</style>