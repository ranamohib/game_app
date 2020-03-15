<template>
  <div class="carousel">
    <h2>{{ title }}</h2>
    <div class="container">
      <carousel :items="6" :dots="false" :responsive="{0:{items:3,nav:false},600:{items:6,nav:true}}">
        <Card v-for="game in games" :key="game.id" :game="game"></Card>
      </carousel>

    </div>
  </div>
</template>

<script>
import Card from './Card.vue'
import carousel from 'vue-owl-carousel'

const key = '7257fad2aa677ccb2ef492c149ec5a63';
const proxy = 'https://cors-anywhere.herokuapp.com/';
const url = 'https://api-v3.igdb.com';
let currentTimeStamp = parseInt((new Date().getTime() / 1000).toFixed(0));


let search = async function(endpoint,fields,filter=""){
                    
    var respone = await fetch(`${proxy}${url}/${endpoint}`,{
    headers:{
    'user-key': key,
    'Conetent-type': 'application/json'
    },
    method: 'POST',
    body: `f ${fields.join(",")};${filter}`
    });
    this.games = await respone.json();
    await console.log(this.games)    
                
}
let test = async function(endpoint,fields,filter=""){
                    
    var respone = await fetch(`${proxy}${url}/${endpoint}`, {
        headers: {
            'user-key': key,
            'Conetent-type': 'application/json'
        },
        method: 'POST',
        body: `f ${fields.join(",")};${filter}`
    });
    respone.json().then(function (r) {
        console.log(r);
    });
}

test("games",["name","cover.url","genres.name","summary"],"w rating > 95;"); 

export default {
  name: 'Carousel',
  props: [
      "game",
      "title"
  ],
  components: {
    Card,
    carousel
  },

  // asyncData ({ params, error }) {
  //   const proxyurl = 'https://cors-anywhere.herokuapp.com/'
  //   return axios.get(`${proxyurl}https://api-v3.igdb.com/games/?fields=name,genres.name,cover.url,popularity&order=popularity:desc&expand=genres`)
  //   .then((res) => {
  //     return {
  //       games: res.data
  //     }
  //   })
  //   .catch((e) => {
  //     console.log(e)
  //   })
  // },
  data() {
    return {
      games: [],

    }  
  },

  methods:{
    search,
           
  },

    mounted(){
            
      this.search("games",["name","cover.url","genres.name","summary","platforms.abbreviation","popularity","release_dates.date"],"where platforms = (48,49,6) & cover != null & release_dates.date > "+currentTimeStamp+";sort popularity desc;");
      // this.search("covers",["url"],"w id = 22963;");
      // "where rating >= 90 & release_dates.date > 631152019;" 
         
    }
}
</script>

<style scoped>
.carousel{
  width: 85%;
  margin: auto;

}
h2{
  margin-bottom: 10px;
}
@media only screen and (max-width: 600px) {
  h2{
    font-size: 16px;
    font-weight: 700;
    margin-bottom: 0;
  }
}
</style>
