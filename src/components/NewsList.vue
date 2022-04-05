<template>

<form class="d-flex flex-column justify-content-center">
 <div class="input-group mx-sm-3 mb-2">
 <label class="visually-hidden" for="search">Search</label>
 <input type="search" name="search" v-model="searchTerm"
id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
search term here" />
 <button class="btn btn-primary mb-2">Search</button>
 </div>
 <p>You are searching for {{ searchTerm }}</p>
 </form>
 
 
 <div class="card">
        <div v-for="article in articles">
            <div class="card-body">
            <img class="art_img" v-bind:src= article.urlToImage />
            <h5>{{ article.title }}</h5>
            <p>{{ article.description }}</p>
            </div>
        </div>
    </div>
    
</template>

<script>
export default { 
    data() {
        return {
            articles: []
            };
    },

created() {
    let self = this;

    fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
            Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
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
       };
</script>

<style>

.card {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-row-gap: 1em;
    width: 65rem;
    margin: center;
}


.art_img{
    object-fit: cover;
    height: 10em;
}

</style>