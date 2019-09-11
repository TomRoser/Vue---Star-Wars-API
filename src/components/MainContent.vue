<template>

    <div>
        <div class="hello">Star Wars Characters</div>

        <button @click="showAllCharacters">Show All characters</button>

        <section v-if="errored">
            <p>No Data :-(</p>
        </section>

        <section v-else>
            <div v-if="loading">Loading...</div>
        </section>

        <div>
            {{ characterList }}
        </div>
  
    </div>

</template>

<script>

export default {
    name: 'MainContent',
        data: function () {
        return {
            characters: [],
            loading: true,
            errored: false,
            characterList: []
        }
    },
    mounted: function() {
            this.$axios
                .get('https://swapi.co/api/people')
                .then(response => {
                this.characters = response.data.results
            }) 
        .catch(error => {
            console.log(error)
                this.errored = true
            })
                .finally(() => this.loading = false)
    },
    methods: {
        showAllCharacters: function () {
            
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
