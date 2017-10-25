<template>
  <div class="news">
    <h2>News</h2>
    <div class="cardContain">
      <div class="card" v-for="news in news" >
        <a :href="news.link" class="link" target="_blank">
          <h3 class="title">{{news.title}}</h3>
          <img :src="news.thumbnail" alt="" class="thumbnail">
        
        <p class="sample"> {{news.description}} </p>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'news',
  data () {
    return {
      news: []
    }
  },
  mounted() {
    axios.get('https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Fabc7ny.com%2Ffeed%2F')
    .then( response => {this.news = response.data.items})
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.cardContain { 
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.card {
  background-color: #667F6d;
	box-shadow: 3px 3px 3px #111;
  color: #fff;
  margin: 1vw;
  width: 20vw;
}

.title, .sample {
  padding: 0 3vw;
}

.thumbnail {
  width: 20vw;
  height: auto;
}

@media (max-width: 950px) {
  .cardContain {
    flex-direction: column;
  }

  .card {
    width: 80vw;
    margin: 1vw 10vw;
  }
  
  .title, .sample {
    text-align: center;
  }

  .thumbnail {
    width: 80vw;
  }

}
</style>
