<template >
   <div> <div class="slider" >
        <div  v-bind:key="fav" v-for="fav in favs" >
<fav-item :id="fav"/>   
      </div>
    </div></div>
</template>
<script>
import FavItem from './FavItem.vue';

export default {
    name: "Favorites",
    components:{


        FavItem
        
    },


    data(){
        return{
            favs:[],
        }
    },
    props:["changed"],
     watch: {
    changed: {
      immediate: true,
      deep: true,
      handler(newValue, oldValue) { 
          console.log(newValue +" "+ oldValue)
          
          this.ListFav();
      }
    }
  },
    mounted(){

            this.ListFav();
       
    },
    methods:{
        ListFav()
        {
            if(localStorage.favs != null){
this.favs= localStorage.favs.split(",");

            }

}
    }
    
}
</script>
<style lang="scss" scoped>
.container {
  display: flex; /* or inline-flex */
  flex-direction: row
}

.slider {
  width: 100%;
  height: 350px;
  display: flex;
  overflow-x: auto;
}

</style>