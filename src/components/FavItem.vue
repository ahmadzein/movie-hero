
<template>
    <div class="slide">
         
     <img v-bind:src="result.Poster == 'N/A'  ? 'https://bighugelabs.com/img/poster-light.jpg' : result.Poster " :key="result.poster" :alt="result.Title">
    
    </div>
</template>
<script>
import axios from 'axios';

export default {
    
    name:"favItem",
    data(){
        return{
        apikey:"2133a611",
        result: ""

        }
    },
    props:["id"],

    methods:{

    },
    mounted(){

       
            axios.get('http://www.omdbapi.com/?i='+this.id+"&apikey="+this.apikey)
      .then(res => 
      {
        this.result = res.data;
        

       console.log("lobe")
      })
      .catch(error => console.log(error))
    }
}
</script>
<style scoped>
img{
    height: 300px !important;
    grid-row: 4;
    
}
.slide {
  width: 300px;
  flex-shrink: 0;
  height: 100%;
}

</style>