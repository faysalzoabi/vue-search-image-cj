<template>
  <div id="app">
    <h1>{{title}}</h1>
    <form @submit.prevent="formSubmitted">
        <label htmlFor="searchTerm">Search Term</label>
        <input v-model="searchTerm" type="text" class="u-full-width" id="searchTerm"/>
        <button type="submit">Search</button>
    </form>
      <div v-if="loading">
        loading...
      </div>
      <section class="images">
         <img v-for="image in images" :key="image.id" :src="image.webformatURL" alt="">
      </section>
  </div>
</template>

<script>
 import axios from 'axios';

export default {
  name: 'app',
  data(){
    return {
      title:'VUE Image Search',
      searchTerm:'',
      images:[],
      loading:false,
    }
  },
  components: {
    
  },
  methods: {
    formSubmitted() {
      console.log('hello');
      this.loading=true;
      this.images=[];
      axios.get(`https://pixabay.com/api/?key=10719673-96a765bfec3365b312bfe2d33&q=${this.searchTerm}&image_type=photo&pretty=true`)
         .then(result => {
           console.log('result', result.data.hits);
           this.images = result.data.hits;
           this.loading=false;
         })

    }
  }
}
</script>

<style>
body{
  width:80%;
  margin: 2em auto 0 auto;
}

img {
  width:100%;
}

.images {
  column-count: 3;
}
</style>
