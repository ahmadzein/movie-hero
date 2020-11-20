<template>
<div >
    <div class="md-layout md-alignment-top-center space">
    <md-table  >
 <md-table-row>
         <md-table-head>Favorite</md-table-head>
        <md-table-head >Poster</md-table-head>
        <md-table-head>Type</md-table-head>
        <md-table-head>Title</md-table-head>
        <md-table-head>Year</md-table-head>
        <md-table-head>imdbID</md-table-head>
      </md-table-row>

      <md-table-row v-bind:key="result.imdbID" v-for="result in results" >
          <md-table-cell> <md-button class="md-icon-button "  v-on:click="addToFav(result.imdbID)">
        <md-icon :class="isFav(result.imdbID) ? 'md-accent' : ''">favorite_border</md-icon>
      </md-button>
    </md-table-cell>
        <md-table-cell md-numeric> <img v-bind:src="result.Poster == 'N/A' ? 'https://bighugelabs.com/img/poster-light.jpg' : result.Poster " :key="result.poster" :alt="result.Title" ></md-table-cell>
        <md-table-cell>{{result.Type}}</md-table-cell>
        <md-table-cell>{{result.Title}}</md-table-cell>
        <md-table-cell>{{result.Year}}</md-table-cell>
        <md-table-cell>      <md-button :href="'https://www.imdb.com/title/'+result.imdbID"  target="_blank" class="md-raised md-primary">View on IMDB</md-button>
</md-table-cell>
      </md-table-row>
    </md-table>
    </div>

    </div>    
</template>
<script>

export default {
    name:"Results",
    data () {
      return {
        currentPage: 1,
        localfav : localStorage.favs,
      }
    },
    props:["results"],
    methods:{
        addToFav(id){
if(localStorage.favs != null){
    console.log(localStorage.favs.includes(id));
      if(localStorage.favs.includes(id) ){
   localStorage.favs = localStorage.favs.replace(id+',','');  

             }else{
   localStorage.favs = localStorage.favs + id +",";  
}
}else{
    localStorage.favs =id +","
}
    event.target.classList.toggle("md-accent") ;
  console.log("emit");
                this.$emit("updated","change");

        },
        isFav(id){

            var mano=id;
            id= mano
            if(localStorage.favs != null){
            if(localStorage.favs.search(id)>1 ){
            return true;
            }else{
            return false;

            }
            
            }
          

        }
    }
    
}
</script>
<style scoped>
img{
    height: 70px !important;
}
md-table-row{
    text-align: center;
}
.space{
    margin: 30px;
}
</style>