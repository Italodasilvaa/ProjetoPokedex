<template>
  <div id="pokemon">
   
    <div class="card">
  <div class="card-image">
    <figure >
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
      <h1 class="title is-4">{{num}} - {{ name | upper }}</h1> 
        <p class="subtitle is-6">Tipo: {{pokemon.type | upper}}</p>
    <div class="media">
      
      <div class="media-content">
          <button class="button " @click="mudarSprite">Mudar Sprite</button>
           <button class="button is-warning " @click="mudarShiny">Mudar Shiny</button>
         
      </div>
    </div>

    <div class="content">
      
    </div>
  </div>
</div>
  </div>
</template>

<script>

import axios from 'axios';



export default {
created:function(){
axios.get(this.url).then(res => {
    
this.pokemon.type = res.data.types[0].type.name;
this.pokemon.front = res.data.sprites.front_default;
this.pokemon.frontShiny = res.data.sprites.front_shiny;
this.pokemon.back = res.data.sprites.back_default;
this.pokemon.backShiny = res.data.sprites.back_shiny;
this.currentImg = this.pokemon.front;
})
},
data(){
    return{
        isFront:true,
        currentImg:'',
        pokemon: {
            type:'',
            front:'',
            frontShiny:'',
            back:'',
            backShiny:''
        }

    }
},

  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters:{
      upper:function(value){
          var newName = value[0].toUpperCase() + value.slice(1);
          return newName;
      }
  },
  methods:{
      mudarSprite: function(){
          if(this.isFront){
              this.isFront = false;
              this.currentImg = this.pokemon.back;
          }else{
              this.isFront = true;
              this.currentImg = this.pokemon.front
          }
      },
      mudarShiny: function(){
          if(this.isFront){
              console.log(this.isFront);
              this.isFront = false;
              this.currentImg = this.pokemon.frontShiny;
          }else{
              this.isFront = true;
              this.currentImg = this.pokemon.backShiny;
          }
      }
  }
};
</script>
<style scoped>

#pokemon{    
    margin-top:2%;
    }
#pokemon:hover{
    top:-2px;
    box-shadow:0 2px 2px #666
    
}
.button{
    margin-right: 10px;
}
</style>