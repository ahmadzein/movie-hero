<template>
  <div>
    <form novalidate class="md-layout md-alignment-top-center" @submit.prevent="validateUser">
      <md-card class="md-layout-item md-size-50 md-small-size-100">
        <md-card-header>
          <div class="md-title">{{title}}</div>
        </md-card-header>

        <md-card-content>
          
          <div class="md-layout md-gutter">
            <div class="md-layout-item md-small-size-100">
              <md-field :class="getValidationClass('search')">
                <label for="search">Title...</label>
                <md-input name="search" id="search" autocomplete="given-name" v-model="form.search" :disabled="sending" />
                <span class="md-error" v-if="!$v.form.search.required">The Title is required</span>
                <span class="md-error" v-else-if="!$v.form.search.minlength">Invalid Title</span>
              </md-field>
            </div>

           
          </div>

   

        
        </md-card-content>

        <md-progress-bar md-mode="indeterminate" v-if="sending" />

        <md-card-actions>
          <md-button type="submit" class="md-primary" :disabled="sending">Search</md-button>
        </md-card-actions>
      </md-card>

      <md-snackbar md-position="left" :md-active.sync="userSaved">Searcched for {{ LastSearch }} and found {{totalResults}} results!</md-snackbar>
    </form>
  </div>
</template>

<script>
  import { validationMixin } from 'vuelidate'
  import {
    required,

    minLength,
 
  } from 'vuelidate/lib/validators' 
import axios from 'axios';

  export default {
    name: 'Search',
    mixins: [validationMixin],
    props:["type","title","page"],
     watch: {
    page: {
      immediate: true,
      deep: true,
      handler(newValue, oldValue) {
console.log(oldValue +" and "+ newValue);
if(this.params.s !="" ){
  this.params.page = newValue;
this.getList();
}
      }
    }
  },
     
      data: () => ({
      form: {
        search: null,

      },
      userSaved: false,
      totalResults: null,
      sending: false,
      LastSearch: null,
      results: null,
      params:{
        page: 1,
        type: "",
        s:"",
        apikey:"2133a611"
      }
    }),
    validations: {
      form: {
        search: {
          required,
          minLength: minLength(3)
        },
       
      }
    },
    methods: {
      PageChanged(){
    
          console.log('Prop changed: ');
        
      },
      getValidationClass (fieldName) {
        const field = this.$v.form[fieldName]

        if (field) {
          return {
            'md-invalid': field.$invalid && field.$dirty
          }
        }
      },
      clearForm () {
        this.$v.$reset()
        this.form.search = null

      },
      
      getList () {
        if(this.type == "all"){
        this.params.type= null;

        }else{
                  this.params.type= this.type;

        }

        this.params.s= this.form.search.trim();
        this.sending = true;
        console.log(this.params);
axios.get('http://www.omdbapi.com/?type='+this.params.type+"&s="+this.params.s+"&apikey="+this.params.apikey+"&page="+this.params.page)
      .then(res => 
      {
        this.results = res.data;
        this.$emit("results",this.results["Search"],this.results["totalResults"])
if(this.results["totalResults"] == null ){
              this.totalResults = "0"

          } else {
                      this.totalResults =this.results["totalResults"];

          }
       console.log("lobe")
      })
      .catch(error => console.log(error))

         window.setTimeout(() => {
          this.LastSearch = `${this.form.search}`

          this.userSaved = true
          this.sending = false

        }, 100) 
      },
      validateUser () {
        this.$v.$touch()

        if (!this.$v.$invalid) {
                    this.params.page =1;
          this.getList()
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .md-progress-bar {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
  }

</style>