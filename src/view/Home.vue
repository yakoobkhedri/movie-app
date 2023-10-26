<template>
  <div class="home">
    <div class="relative">
      <router-link :to="{name:'Movie Detail',params:{id:'tt0409591'}}">
        <img class="w-full h-96 object-cover relative" alt="poster"
          src="../assets/img/naruto-poster-kakashi-64nd375j6nkyxw1c.jpg">
        <div class="absolute left-0 right-0 bottom-0 p-4 z-10 bg-black opacity-60">
          <h3 class="text-white mb-4">Naruto</h3>
          <p class="text-white">
            Naruto[a] is a Japanese manga series written and illustrated by Masashi Kishimoto.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="flex items-center justify-center flex-col p-4">
      <input v-model="search"
        class="focus:shadow-lg placeholder:text-[#f3f3f3] rounded-lg mb-4 transition-all duration-200 bg-none border-none outline-none appearance-none text-white p-4 text-xl w-full bg-[#496583]"
        placeholder="What are you looking for?">
      <input
        class="w-full max-w-xs  bg-[#42b883] p-4 rounded-lg text-xl text-white uppercase border-none transition-all duration-200 active:bg-[#3b8070] cursor-pointer outline-none appearance-none"
        type="submit" value="Search">
    </form>

    <div class="grid xl:grid-cols-4 lg:grid-cols-3 sm:grid-cols-2 gap-5">
      <div v-for="movie in movies" :key="movie.imdbID" class="w-fuul">
        <router-link :to="'/movie/' + movie.imdbID">
          <div class="relative">
            <img alt="movie poster" :src="movie.Poster" class="w-full h-80 object-cover">
            <div class="absolute py-2 px-4 bg-[#42b883] text-white bottom-4 left-0 capitalize">{{ movie.Type }}</div>
          </div>
          <div class="bg-[#496583] py-4 px-2 rounded-b-lg">
            <p class="text-[#aaa] text-sm">{{ movie.Year }}</p>
            <h3 class="text-white text-lg font-semibold">{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '../env.js'

export default {

  setup() {
    const search = ref('');
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != '') {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = '';
          },)
      }
    }


    return {
      search,
      movies,
      SearchMovies
    }
  }


}
</script>

<style></style>