<script>
/* 
  Per importare ed utilizzare un componente dentro un altro devo SEMPRE seguire questi 3 passi:
  1) Importazione del componente
  2) Dichiarazione del componente
  3) Utilizzo del componente
*/
// 1) Importazione del componente
import AppHeader from './components/AppHeader.vue';
import axios from 'axios';

export default {
  data() {
    return { 
      searchText:'',
      apiKey: 'c226b46bed5e65374d45ee2f2efb7ee9',
      movies: [] ,
     
    }
  },
  // 2) Dichiarazione del componente
  components: {
    AppHeader
  },
  methods: {
    search(){
      // oppure con il metodo più semplice
      // .get('https://api.themoviedb.org/3/search/movie?api_key= ' + this.apiKey + '&query=' + this.searchText) 

      axios
      .get('https://api.themoviedb.org/3/search/movie', {
        params : {
          api_key: this.apiKey,
          query: this.searchText,
        }
    })
      .then((res) => {
        // console.log(res);
        console.log(res.data);
        // console.log(res.data.results);
        this.movies = res.data.results;
      });

      this.searchText = '';
    }
   
  }
}
</script>

<template>
  <div>
    <!-- 3) Utilizzo del componente -->
    <AppHeader />
    
    <div class="d-flex justify-content-between p-20">
      <div>
        <form @submit.prevent.enter="search()">
          <input  v-model="searchText" type="text" placeholder=" Insert your movie" class="text-center">
          <button  type="submit" class="btn btn-secondary">
            near
          </button>
        </form>
      </div>
      <!-- <div>
        <input v-model="searchText" type="text" placeholder=" Insert your serie" class="text-center"  > 
        <button @click.prevent="search()" type="submit" class="btn btn-secondary">
          near
        </button>
      </div> -->
    </div>

    <div>
      <ul v-for="(movie ,i) in movies">
        <li >
          Titolo : {{ movie.title }}
        </li>
        <li>
          Titolo Originale: {{ movie.original_title }}
        </li>
        <li>
          Lingua: {{ movie.original_language }}
        </li>
        <li>
          Voto: {{ movie.vote_average }}
        </li>
      </ul>
    </div>
  
  
  </div>
</template>

<style lang="scss" >
@use 'assets/scss/main' as *;
// Import all of Bootstrap's CSS
@import "bootstrap/scss/bootstrap";
div button{
  width: 100px;
  margin-left: 10px;
}
.p-20{
  padding: 20px;
}







</style>
