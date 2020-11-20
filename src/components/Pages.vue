
<template>
<div>
<div class="md-layout md-alignment-top-center">

<md-button class="md-icon-button md-raised" :disabled=" currentPage < 3" v-on:click="changePage(bl)">
        <md-icon>keyboard_arrow_left</md-icon>
      </md-button>
      <md-button class="md-icon-button md-raised " :class="currentPage == b1 ? 'md-primary' : ''" v-on:click="changePage(b1)" >
        {{b1}}
        </md-button>
        <md-button class="md-icon-button md-raised"  :class="currentPage == b2 ? 'md-primary' : ''" v-on:click="changePage(b2)" :disabled=" totalResults <=10 ">
        {{b2}}
        </md-button>
        <md-button class="md-icon-button md-raised" :class="currentPage == b3 ? 'md-primary' : ''" v-on:click="changePage(b3) " :disabled="totalResults <=20  ">
        {{b3}}
        </md-button>
      <md-button class="md-icon-button md-raised" v-on:click="changePage(br)" :disabled=" currentPage+3 > (totalResults/10) ">
        <md-icon>keyboard_arrow_right</md-icon>
      </md-button>


      </div>
      </div>
</template>
<script>

export default {
    name:"Pages",
    data () {
      return {
        bl: null,
        b1: null,
        b2: null,
        b3: null,
        br: null,
        currentP : this.currentPage
      }
    },
    props:["currentPage","totalResults"],
  
    mounted(){
        this.SetNumbers();
  },
  methods:{
            SetNumbers(){
   console.log(this.currentP);

   if (parseInt(this.currentP)<4){
this.bl=1;
this.b1=1;
this.b2=2;
this.b3=3;

   }else{
  if(parseInt(this.currentP)-3 < 1){
      this.bl=1;
}else{
this.bl = parseInt(this.currentP)-3;
}      
this.b1=parseInt(this.currentP)-1;
      this.b2=parseInt(this.currentP);
      this.b3=parseInt(this.currentP)+1;

 
   }
         if(parseInt(this.currentP)+3 > parseInt(this.currentP)){
      this.br=parseInt(this.currentP)+3;
}else{
this.br = parseInt(this.currentP);
}
   console.log(this.currentP);

            },
      changePage(page){
          this.currentP=page;
          this.$emit("changePage",page);
 this.SetNumbers();
      }
  }
    
}
</script>