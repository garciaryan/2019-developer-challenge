<template>
  <div class="container">
    <div class="search-container">
      <label for="breeds">Search for a dog!</label>
      <input 
          class="search-bar" 
          id="breeds" 
          type="text" 
          v-model="search"
          @focusin="isActive = true" 
          @focusout="isActive = false"
          @keyup="searchBreeds()"
      />

    </div>
    <div v-if="isActive" class="dropdown">
      <div class="results-container" 
        v-for="breed in filteredBreeds" 
        :key="breed.breedId"
      > 
        <h4>{{ breed.breedName }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name:  'Autosuggest',

  data(){
    return {
      search: '',
      breeds: [],
      filteredBreeds: [],
      isActive: false
    }
  },

  mounted(){
    axios.get('https://ra-api.adoptapet.com/v1/pet-utilities/1/breeds')
    .then(res => {
      this.breeds = res.data.body;
    })
    .catch(err => { throw err; })
  },

  methods: {
    searchBreeds(){
      this.filteredBreeds = this.breeds.filter(breed => {
        if (breed.breedName.includes("")){
          let breedName = breed.breedName.replace(/"/g,"");
          return breedName.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
        } else {
          return breed.breedName.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
        }
      })
      return this.filteredBreeds;
    }
  }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Raleway:300,400');

  .container {
    height: 200px;
    width: 66%;
    .search-container {
      width: 100%;

      label {
        display: flex;
        padding-bottom: 7px;
      }

      .search-bar {
        width: 100%;
        height: 50px;
        display: block;
        background-clip: padding-box;
        border: 1px solid #ced4da;
        border-radius: .25rem;
        font-size: 25px;
        color: #000;
      }
    }

    .dropdown {
      display: flex;
      width: 100%;
      border-bottom-left-radius: 5px;
      border-bottom-right-radius: 5px;
      box-shadow: 0 4px 2px -2px gray;
      flex-direction: column;
      justify-content: space-between;
      overflow: scroll;
      background-color: #00A8DD;

      .results-container {
        &:hover {
          background-color: gray;
        }

        h4 {
          width: 98%;
          height: 100%;
          display: flex;
          color: #fff;
          padding-left: 10px;
          font-family: 'Raleway', sans-serif;
          font-weight: 300;
        }
      }
    }
  }

</style>
