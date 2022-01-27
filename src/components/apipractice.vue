<template>
  <div>

    <input type="number"  class=" mt-2 mx-auto col-4"  placeholder="id" v-model="id" > {{id}} <br>
    <input type="text" class=" mt-2 mx-auto col-4"  placeholder="name" v-model="name"  > {{name}} <br>
    <input type="number"  class=" mt-2 mx-auto col-4" placeholder="price" v-model="price"  > {{price}} <br>
    <button v-on:click="ADD" class="btn btn-dark"> ADD </button>


       <h2> Products</h2>
       <!-- {{proData}} -->
       <h6 >
         <table class="table ">
           <tr>
             <td>ID</td>
             <td>EMAIL</td>
             <td>NAME</td>
             <td>Action</td>
           </tr>
           <tr  v-for="pro of proData" :key="pro.id">
      <td>   {{pro.id}}  </td>
        <td> {{pro.price}} </td>
       <td>  {{pro.name}} </td>
    <td><button class=" btn btn-primary" v-on:click="delPro(pro.id)">Delete</button></td>
       
            
           </tr>
          
         </table>
       </h6>
    <br><br>
  
  </div>
</template>

<script>
    // import axios from 'axios'
    // import Vue from 'vue'
    // import VueAxios from 'vue-axios'
    // Vue.use(VueAxios.axios)
    // import Vue from 'vue';
    // import VueAxios from 'vue-axios';
    import axios from 'axios';
    // Vue.use(VueAxios,axios);
    
export default {
  name:"Apipractice",
  data(){
      return {proData:undefined,id:'',name:'',price:''}
  },
  mounted()
  {
      axios.get("http://localhost:300/product")
      .then(res=>{
        // console.log(res.data)
        this.proData=res.data
      })
  },
   methods:{
      delPro(id){
           const URL="http://localhost:300/product/";
          if(confirm("Do u want to delete it ?")){
              axios.delete(`${URL}${id}`)
              .then(res=>{
                  if(res){
                       axios.get(URL)
                       .then(res=>{
                         this.proData=res.data;
                     })
                  }
              })
          }
      },
      ADD()
      {
          const URL="http://localhost:300/product/";
          const article = { id: this.id , name:this.name , price:this.price}
          axios
          .post(URL,article)
          
 axios.get("http://localhost:300/product")
      .then(res=>{
        // console.log(res.data)
        this.proData=res.data
      })

          


      }
  
      
  }

   
}
</script>

<style>

</style>