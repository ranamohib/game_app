<template>
  <div id="">
    <Card v-for="game in games" :game="game" :key="game.id"></Card>
  </div>
</template>

<script>
import Card from './Card.vue'

const key = '7257fad2aa677ccb2ef492c149ec5a63';
const proxy = 'https://cors-anywhere.herokuapp.com/';
const url = 'https://api-v3.igdb.com';

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
      "game"
  ],
  components: {
    Card
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
      games: []
    }  
  },

  methods:{
    search,
           
  },

    mounted(){
            
      this.search("games",["name","cover.url","genres.name","summary"],"w rating > 95;");
      // this.search("covers",["url"],"w id = 22963;");
      // "where rating >= 90 & release_dates.date > 631152019;" 
         
    }
}
</script>

<style>

</style>
