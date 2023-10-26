<template>
  <div class="p-4">
   <h2 class="text-white text-3xl font-semibold mb-4">{{ movie.Title }}</h2>
   <p class="text-white text-lg leading-6">{{ movie.Year }}</p>
   <img class="mb-4 max-w-[200px] block" alt="Movie Poster" :src="movie.Poster">
   <p class="text-white text-lg leading-6">{{ movie.Plot }}</p>
  </div>
</template>

<script>
import {ref,onBeforeMount} from 'vue'
import { useRoute } from 'vue-router';
import env from '../env.js';

export default {

 setup(){
  const movie= ref({});
  const route= useRoute();

  onBeforeMount(()=>{
    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
    .then(response=>response.json())
    .then(data=>{
      movie.value=data;
    })
  });

  return{
    movie
  }

 }

}
</script>

<style>

</style>