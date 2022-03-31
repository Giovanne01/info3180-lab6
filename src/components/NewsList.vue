

<template>
    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search </label>
            <input type="search" name="search" v-model="searchTerm" id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
    </form>

    <div class="cont">
        <div v-for="article in articles" class="card">
            <div class="top">
                <img class="card-img" v-bind:src="article.urlToImage" :alt="article.title" />
            </div>
            <div class="bottom">
                <h5>{{ article.title }}</h5>
                <p>{{article.description}}</p>
            </div>

        </div>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            articles:[],
            searchTerm: ''
            
        };
    },
    methods: {
 searchNews() {
 let self = this;
 fetch('https://newsapi.org/v2/everything?q='+
self.searchTerm + '&language=en', {
 headers: {
 'Authorization': `Bearer $
{import.meta.env.VITE_NEWSAPI_TOKEN}`,
 }
})
 .then(function(response) {
 return response.json();
 })
 .then(function(data) {
 console.log(data);
 self.articles = data.articles;
 });
 }
 },



    created() {
        let self=this;
        fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
    headers: {
        'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
    }
})
        .then(function(response) {
            return response.json();
        })
        .then(function(data) {
            console.log(data);
            self.articles = data.articles;
        });
    }
}
</script>

<style>
 @import '@/assets/styles.css';

</style>


 