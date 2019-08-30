<template>
  <div class="hello">
    
    <div id="btn_show_all">
      <button @click="loadCharacters">Show all Characters</button>
    </div>
    
    <input placeholder="Suchanfrage" @keyup="search()" v-model="query" ><button >Search for Character</button>
   
    <div>Searching for: {{query}}</div>

    <div class="character_container">
        <div class="no_results" v-if="characters.length === 0">Keine Ergebnisse</div>
        <div class="character_card" v-for="character in characters" v-bind:key="character.name">
          <span>Name:{{character.name}}</span> <br>
          <span>Height: {{character.height}}</span> <br>
          <span>Mass: {{character.mass}}</span> <br>
          <span>Hair Color: {{character.hair_color}}</span> <br> 
        </div> 
    </div>

  </div>
</template>

<script>

export default {
    name: 'MainContent',
    data: function () {
      return {
      characters: [],
      query: ''
      }
    },
    methods: {
      loadCharacters: function() {
        this.$axios
          .get('https://swapi.co/api/people')
          .then(response => {
            this.characters = response.data.results
            })   
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.character_card {
  border: solid;
  display: inline-block;
  margin: 2%;
}
#btn_show_all {
  display: block;
  text-align: center;
}

</style>
