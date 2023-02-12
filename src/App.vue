<script setup>
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

import { ref, computed, onMounted } from 'vue'
const postXpage = 5;
const  inicio = ref(0);
const  fin = ref(postXpage);
const loading = ref(true);

const next = () => {
    inicio.value  += +postXpage;
    fin.value += +postXpage;
}
const prev = () => {
    inicio. value += -postXpage;
    fin.value +=  -postXpage;
}

const posts = ref([]);

// fetch('https://jsonplaceholder.typicode.com/posts') //fetch es una promesa

// no se recomienda usar onmounted para hacer fetch
/*onMounted(async() => {
    //loading.value = true;
   try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts')
    //const data = await response.json();
    posts.value = await response.json();
   } catch (error) {
       console.log(error)
   } finally {
       loading.value = false;
   }

})*/

// se recomienda usar async await y es la mejor forma de consumir apis
const fetchData = async () => {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts')
        //const data = await response.json();
        posts.value = await response.json();
       } catch (error) {
           console.log(error)
       } finally {
           loading.value = false;
       }
}

fetchData();

/*
fetch sin async await onMounted
fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())
    .then(data => posts.value = data)
    .finally(() => loading.value = false)*/
const favoritePost = ref("");

const addFavoritePost = (title) => {
    favoritePost.value = title;
}

const finPost = computed(() => {
    return posts.value.length;
})


</script>
<template>
<LoadingSpinner v-if="loading"/>
<div class="container mx-auto d-flex flex-column" v-else="loading">
    
    <div class="row" >
        <div class="col-12">
            <h1>Mi Post Favorito es:  {{ favoritePost }} </h1>
        </div>
        
        <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :finPost="finPost" class="mb-2"/>
    </div>
   
    <div class="row">
        <div class="col-12">
            <BlogPost v-for="post in posts.slice(inicio, fin)" 
            :key="post.id" 
            :title="post.title" 
            :id="post.id" 
            :body="post.body" 
            :colorText="post.colorText"
            @addFavoritePost="addFavoritePost"  class="mb-2"/>
        </div>
    </div>


   <!-- <BlogPost 
    title="Post 1" id="1" body="descripcion-1" colorText="primary"/>
    <BlogPost
    title="Post 2" id="2" body="descripcion-2" colorText="info"/>
    <BlogPost
    title="Post 3" id="3"  colorText="success"/>
    <BlogPost
    title="Post 4" id="4" body="descripcion-4" colorText="warning"/>-->
</div>
   
    
   
    
     </template>

