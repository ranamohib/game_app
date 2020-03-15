<template>
  <div class="card"> 
        <div class="gradient"></div>
        <img :src="'https:' + game.cover.url.replace('t_thumb', 't_cover_big')">
        <span class="tag">{{ platforms }}</span>
        <p>{{game.name}}</p>
    </div>
</template>

<script>


export default {
  name: 'Card',
  props: ['game'],
  computed: {

  genres: function () {
      let i;
      let genres = "";
      for(i=0; i<this.game.genres.length; i++){
        genres += this.game.genres[i].name;
      }
      return genres
    },
  platforms: function () {
      let i;
      let platforms = "";
      for(i=0; i<this.game.platforms.length && i<3; i++){
        platforms += ` ${this.game.platforms[i].abbreviation}`;
      }
      return platforms
    }
  }
}
</script>
<style scoped>
.card{
  width: 175px;
  height: 233px;
  overflow: hidden;
  position: relative;
  border-radius: 5px;
  margin: 8px;
  cursor: pointer;
  box-shadow: 0 0 0 rgba(80,216,144,0.4);
  background: black;
}
.card:hover{
    -moz-animation: pulse 2s infinite;
    -webkit-animation: pulse 2s infinite;
    animation: pulse 2s infinite;
}
@keyframes pulse {
    0% {
        box-shadow: 0 0 0 0 rgba(80,216,144,0.4);
    }
    70% {
        box-shadow: 0 0 0 10px rgba(80,216,144,0);
    }
    100% {
        box-shadow: 0 0 0 0 rgba(80,216,144,0);
    }
}



.card img{
  width: 100%;
  position: absolute;
  transform: translate(-50%,-50%);
  top: 50%;
  left: 50%;
  z-index: 2;
}
.card div{
  position: absolute;
  width: 100%;
  height: 100%;
  
background: rgb(0,0,0);
background: linear-gradient(180deg, rgba(0,0,0,1) 0%, rgba(255,255,255,0) 25%, rgba(241,238,238,0) 75%, rgba(0,0,0,1) 100%);
  z-index: 3;
}
.card span{
  background: #50d890;
  
  border-radius: 3px;
  color: #222;
  font-size: 11px;
  font-weight: 500;
  height: auto;
  line-height: normal;
  padding: 4px 6px;
  position: absolute;
  right: 8px;
  top: 8px;
  width: auto;
  z-index: 4;
}
.card p{
  
    font-weight: 700;
    font-size: 14px;
    text-align: center;
    color: #fff;
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: auto;
    padding: 10px;
    z-index: 5;

}
@media only screen and (max-width: 600px) {
  .card {
    width: 90px;
    height: 120px;
    border-radius: 0;
  }
  .card span{
    visibility: hidden;
  }
  .card p{
    visibility: hidden;
  }
}
</style>


