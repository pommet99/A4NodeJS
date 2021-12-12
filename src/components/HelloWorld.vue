<template>
  <div>
    <img src="../assets/Pokemon-Symbole.jpeg" class="logo">

    <input v-on:change="changePk" type="number" value="1" class="pokemonNum" placeholder="Research Pokemon ID">

    <div class="pokemonCard">
      <img :src="this.image">
      <p><strong>Name:</strong> {{this.name}}</p>
      <p><strong>Id:</strong> {{this.id}}</p>
      <p><strong>Height:</strong> {{this.height}}</p>
      <p><strong>Weight:</strong> {{this.weight}}</p>
      <p><strong>Type:</strong> <li v-for="value in this.types">{{value.type.name}}</li></p>
    </div>

  </div>
</template>



<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      show: true,
      name:null,
    }
  }, methods:{
    logg: function(event){
    console.log("Test")
},
  changeImage: function(event){
    var i = document.getElementById("imageSource");
    if (i.src == "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Image_created_with_a_mobile_phone.png/250px-Image_created_with_a_mobile_phone.png"){
      i.src = "https://d1fmx1rbmqrxrr.cloudfront.net/cnet/optim/i/edit/2019/04/eso1644bsmall__w770.jpg";
      console.log(i.src);
    } else {
      i.src = "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Image_created_with_a_mobile_phone.png/250px-Image_created_with_a_mobile_phone.png"
    }
  },
changePk: function(event){
  var url = "https://pokeapi.co/api/v2/pokemon/" + event.target.value
  console.log(url)

  axios
      .get(url)
      .then(response => {
        this.name = response.data.name
        this.image = response.data.sprites.front_default
        this.height = response.data.height
        this.types = response.data.types
        this.weight = response.data.weight
        this.id = response.data.id
})
  }
},

  mounted() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/1")
      .then(response => {
        this.name = response.data.name
        this.image = response.data.sprites.front_default
        this.height = response.data.height
        this.types = response.data.types
        this.weight = response.data.weight
        this.id = response.data.id
})
  },

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only

-->
<style scoped>

.logo{
  width: 40vw;
  display: block;
  margin:auto;
}

.pokemonNum{
  margin-bottom: 5vh;
  width: 25vw;
  height: 5vh;
  border: 4px solid black;
  border-radius: 4%;
  font-family: Verdana, sans-serif;
}

.pokemonCard{
    text-transform: uppercase;
    background-color: white;
    width: 40vw;
    display: block;
    margin: auto;
    border-radius: 10%;
    padding-bottom: 3vh;
    margin-bottom: 20vh;
    border: 5px solid black;
    font-family: Verdana, sans-serif;
}

.pokemonCard img{
    width: 15vw;
}

</style>
