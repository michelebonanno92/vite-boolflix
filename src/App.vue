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
      series: [] ,
    
    }
  },
  // 2) Dichiarazione del componente
  components: {
    AppHeader
  },
  methods: {
    search(){
      // axios
      // .get('https://api.themoviedb.org/3/search/movie?api_key=' + this.apiKey + '&query=' + this.searchText) 
   
      // .then((res) => {
      //   console.log(res.data)
      //   this.movies = res.data.results;
      // });
      // this.searchText = '';

      axios
      .get('https://api.themoviedb.org/3/search/movie', {
        params : {
          api_key: this.apiKey,
          query: this.searchText,
        }
      })
      .then((res) => {
        this.movies = res.data.results;
      })
        // this.searchText = '';
      

      axios

      .get('https://api.themoviedb.org/3/search/tv', {
        params : {
          api_key: this.apiKey,
          query: this.searchText,
        }
      })
      .then((res) => {
        this.series = res.data.results;
      })
        // this.searchText = '';
      },
    

    // changeToFlag(lang){
    //   console.log(lang)
    //   const validLangs = [
    //     'en',
    //     'it',
    //     'ja',
    //   ];

    //   if (validLangs.includes(lang)) {
    //     if (lang == 'ja'){
    //       return '/img/jp.png';
    //     }
    //     else {
    //       return '/img/' + lang + '.png';
    //     }
    //   }
    //   else {
    //       return '/img/gm.png';
    //     }
    // },

    // oppure
    getFlagWithObj(lang){
      const validLangs = {
        en: 'en.png',
        it: 'it.png',
        ja: 'jp.png',
      };
      if(lang in validLangs){
        return '/img/' + validLangs[lang];
      }
      else {
        return '/img/gm.png';
      }
    }
  },
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
      <div>
        <input v-model="searchText" type="text" placeholder=" Insert your serie" class="text-center"  > 
        <button @click.prevent="search()" type="submit" class="btn btn-secondary">
          near
        </button>
      </div>
    </div>
<div class="d-flex justify-content-between p-20">
  <div>
      <ol>
        <li v-for="(movie ,i) in movies" :key="i">
          <ul>
            <li >
              Titolo : {{ movie.title }}
            </li>
            <li>
              Titolo Originale: {{ movie.original_title }}
            </li>
            <!-- sostituiamo la lingua originale da stringa ad una immagine atraverso una funzione che avrà come paramentro la lingua originale  -->
            <li>
              Lingua: <img :src="getFlagWithObj(movie.original_language)" alt="bandiera">
            </li>
            <li>
              Voto: {{ movie.vote_average }}
            </li>
            <hr>
          </ul>
        </li>
      </ol>
    </div>

    
    <div>
      <ol>
        <li v-for="(serie ,i) in series" :key="i">
          <ul>
            <li >
              Titolo : {{ serie.name }}
            </li>
            <li>
              Titolo Originale: {{ serie.original_name }}
            </li>
            <!-- sostituiamo la lingua originale da stringa ad una immagine atraverso una funzione che avrà come paramentro la lingua originale  -->
            <li>
              Lingua: <img :src="getFlagWithObj(serie.original_language)" alt="bandiera">
            </li>
            <li>
              Voto: {{ serie.vote_average }}
            </li>
            <hr>
          </ul>
        </li>
      </ol>
    </div>
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
