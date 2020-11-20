<template>
  <div class="Movies">

    <Favorites :changed="this.change" :hidden="!isfav" />
    <Search type="movie" title="Search Movies" :page="page" v-on:results="ShowResults"/>
   
    <Results :results="results" :hidden="results == null" v-on:updated="changefav"/>
    <Pages :currentPage="page" :totalResults="totalResults" :hidden="results == null" v-on:changePage="ChangePage"/>
  </div>
</template>

<script>
import Search from '@/components/Search'
import Results from "@/components/Results";
import Pages from "@/components/Pages"
import Favorites from "@/components/Favorites"
export default {
  name: 'Movies',
    data: () => ({
    results : null,
    totalResults : null,
    page: 1,
    change:false,
    isfav:false,
  }),
  components: {
    Search,
    Results,
    Pages,
    Favorites
  },
  methods:{
    ShowResults(results,totalResults){
      console.log(totalResults);
      this.results =results;
      this.totalResults = totalResults;
console.log();
    },
    ChangePage(p){
this.page =p;
    },
    changefav(){
    this.change = !this.change;
    this.checkFav();

},

       checkFav()
        {
            if(localStorage.favs == null || localStorage.favs == "" || localStorage.favs == " " || localStorage.favs.length < 1  ){
           this.isfav=false;

           }else{
              this.isfav=true;

            }
            console.log("his.isfav---------");
            console.log(this.isfav);
            console.log(localStorage.favs.length);
            console.log("this.isfav--------");

}
  },
  mounted(){
    this.checkFav();
  }

}
</script>


