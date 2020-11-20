<template class="ListItem">
    <div>
      <h3>hello</h3>
    </div>
</template>
<script>
export default {
    name: "ListItem",
    props:["fav","poster","type","title","year","id"],
    data(){
        return {
        redHeart: false,
        }
    },
     methods:{
        addToFav(id){
             if(localStorage.favs.search(id)>1 ){
   localStorage.favs = localStorage.favs.replace(id+',','');  

             }else{
   localStorage.favs = localStorage.favs + id +",";  
}
    this.redHeart = !this.redHeart;

        },

      
     }
}
</script>