<template>
  <div class="pokemon-card">
        <div class="card">
            <div class="card-image">
                <figure>
                <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{num}} {{nome | upper}}</p>
                    <p class="subtitle is-6">{{pokemons.type}}</p>
                </div>
                </div>

                <div class="content">
                    <button @click="mudarSprite" class="button is-medium">Mudar sprite</button>
                </div>
            </div>
        </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    created: function ()  {
            axios.get(this.url).then((res) =>{
                this.pokemons.type = res.data.types[0].type.name
                this.pokemons.front = res.data.sprites.front_default
                this.pokemons.back = res.data.sprites.back_default
                this.currentImg = this.pokemons.front
                console.log(this.pokemons)
            })
    },
    data (){
        return{
            isFront: true,
            currentImg: '',
            pokemons: {
                type: '',
                front: '',
                back: ''
            }
        }
    },

    props:{
        num: Number,
        nome: String,
        url: String,
    },
    filters:{
        upper: function(value){
            let newName = value[0].toUpperCase() + value.slice(1)
            return newName
        }
    },
    methods:{
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false
                this.currentImg = this.pokemons.back
            }
            else{
                this.isFront = true
                this.currentImg = this.pokemons.front
            }
        }
    }
}
</script>

<style>
    .pokemon-card{
        margin-bottom: 8px;
    }
</style>