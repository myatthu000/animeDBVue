<template>
  <div class="app">
    <header>
      <h1>The<strong>Anime</strong>Database </h1>

        <form class="search-box" @submit.prevent="HandleSearch">
          <input type="search" 
              v-model.trim="searchQuery"
              class="search-field"
              placeholder="Search for an Anime ....."
              required>
        </form>
    </header>

    <main>
      
      <div class="no-results" v-if="animeList.length == 0">
        <h4>Sorry, we have no results ......</h4>
      </div>

      <div class="cards" v-else>
        <VCard v-for="anime in animeList" :key="anime.mal_id" :anime="anime"></VCard>
      </div>
    </main>
    
  </div>
</template>

<script>
 /* eslint-disable */ 
import {ref} from 'vue';
import VCard from "./components/VCard.vue";


  export default {
  
    components: { VCard },
    setup(){

      let searchQuery = ref("");
      let animeList = ref([]);

      let HandleSearch = async () => {
            animeList.value = await fetch(`https://api.jikan.moe/v3/search/anime?q=${searchQuery.value}`)
              .then(response => response.json())
              .then(data => data.results);

        console.log( animeList.value )
      }
        return {VCard,searchQuery,animeList,HandleSearch}

    }


}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Mukta:wght@200;300;400;500;600;700;800&family=Outfit:wght@100;200;300;400;500;600;700;800;900&display=swap');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Mukta', sans-serif;
  font-family: 'Outfit', sans-serif;
}
a{
  text-decoration: none;
}

header{
  padding-top: 50px;
  padding-bottom: 50px;

  h1{
    text-align: center;
    color: #888;
    font-size: 42px;
    font-weight: 400;
    text-transform: uppercase;
      strong{
        color: #313131;
      }
  }
  .search-box{
    display: flex;
    justify-content: center;
    align-items: center;
    padding-left: 30px;
    padding-right: 30px;

      .search-field{
        appearance: none;
        background: none;
        border: none;
        outline: none;

        background-color: #f3f3f3;
        box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);

        display: block;
        width: 100%;
        max-width: 600px;
        padding: 15px;
        border-radius: 8px;

        color: #313131;
        font-size: 20px;

        transition: 0.4s;

        &::placeholder{
          color: #AAA;

        }

        &:focus, &:valid{
          color: #fff;
          background-color: #313131;
          box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);

        }

      }
    }

}

main{

  max-width: 1200px;
  margin: auto;
  padding-left: 30px;
  padding-right: 30px;

  .cards{
    display: flex;
    flex-wrap: wrap;
    margin: 0 -8px;
    border: 2px solid black;
  }
}

</style>