<template>
<section id= "article_content">
    <div class="card">
        <div v-for="article in articles">
            <img class="art_img" v-bind:src= article.urlToImage />
            <div class="card-body">
            <h5>{{ article.title }}</h5>
            <p>{{ article.description }}</p>
            </div>
        </div>
    </div>
</section>
    
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

section#article_content {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-row-gap: 1em;
}

.card{
    width: 20rem;
    margin: auto;
}

.card-body{
    display: flex;
    flex-flow: row wrap;
    align-items: flex-start;
}

.art_img{
    object-fit: contain;
    height: 10em;
}

</style>