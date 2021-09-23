<template>
  <div class="articles-wrap">

    <div class="articles-box">
        <div class="articles-item" v-for="(article, id) in articlesLocal" :key="id">

          <div class="articles-image">
            <img :src="article.image" />
          </div>

          <div class="articles-date">
            {{article.date}}
          </div>

          <a :href="article.slug" target="_blank" class="articles-title">
            {{article.title}}
          </a>

        </div>
     </div>
       
      <a href="#" class="btn" @click.prevent="getNextArticles()">Показать ещё</a>
  </div>
</template>

<script>

import axios from 'axios';
export default {
    props: {
        isElVisible: {require: false}, 
        articles: {
            require: true
        }
    },
    data() {
    return {
        articlesLocal: this.articles
        }
    },

    methods: {
        getInitialArticles() {
            axios.get(`https://api.blog.vipplay.ru/wp-json/vip/v1/articles/?per_page=24`).then((response) => {
            this.articlesLocal = response.data.articles;
            });
        },

        getNextArticles(i, lengthArticles) {
            lengthArticles = this.articlesLocal.length;
            axios.get(`https://api.blog.vipplay.ru/wp-json/vip/v1/articles/?per_page=24&offset=${lengthArticles}`).then(response => {
                
                for (i = 0; i < response.data.articles.length; i++) {
                    this.articlesLocal.push(response.data.articles[i]);
                }
           
            });
        },
    },
    mounted() {
        this.getInitialArticles();
    }
}

</script>

<style lang="scss" scoped>

.articles-wrap {
  padding: 30px 150px;
}
.articles-box {
  display: flex;
  justify-content: space-between;
  align-items: stretch;
  flex-wrap: wrap;
}
.articles-item {
  max-width: 350px;
  width: 100%;
  margin: 0 15px;
  margin-bottom: 30px;
  padding-bottom: 10px;
  border: 2px solid blue;
  border-radius: 3px;
  overflow: hidden;
  box-sizing: border-box;
}
.articles-image {
  position: relative;
  height: 0;
  padding-bottom: 75%;
  margin-bottom: 15px;
  img {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }
}
.articles-date {
  font-size: 15px;
  padding: 0 0 10px 0;
  border-bottom: 1px solid blue;
  margin-bottom: 15px;
}
.articles-title {
  display: block;
  font-weight: 700;
  text-align: center;
  padding: 0 15px;
  font-size: 18px;
  text-decoration: none;
  color: #000;
  &:hover {
    text-decoration: underline;
  }
}
.btn {
  display: block;
  max-width: 250px;
  margin: 0 auto;
  padding: 25px 50px;
  text-align: center;
  background: rgb(9, 110, 224);
  border-radius: 5px;
  color: #fff;
  text-decoration: none;
  font-size: 18px;
  font-weight: 700;
}
</style>