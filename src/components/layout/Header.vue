<template>
    <div>
        <h1>The Video Searcher</h1>
        <div id="nav">
       <md-button to="/" class="md-accent">Home</md-button>
       <md-button to="/movies" class="md-accent">Movies</md-button>
       <md-button to="/series" class="md-accent">Series</md-button>
    </div>
    <router-view/>
    </div>
</template>

<script>
export default {
    name : "Header",

}
</script>