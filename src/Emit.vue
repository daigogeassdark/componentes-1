<script setup>
import BlogPost from './components/BlogPost.vue';

import { ref } from 'vue'

const posts = ref(
    [
        {
            id: 1,
            title: 'Post 1',
            body: 'descripcion-1',
            colorText: 'primary'
        },
        {
            id: 2,
            title: 'Post 2',
            body: 'descripcion-2',
            colorText: 'info'
        },
        {
            id: 3,
            title: 'Post 3',
            
            colorText: 'success'
        },
        {
            id: 4,
            title: 'Post 4',
            body: 'descripcion-4',
            colorText: 'warning'
        }
    ]
);
const favoritePost = ref("");

const addFavoritePost = (title) => {
    favoritePost.value = title;
}


</script>
<template>

<div class="container">
    <div class="row">
        <div class="col-12">
            <h1>Mi Post Favorito es:  {{ favoritePost }} </h1>
        </div>
    </div>
   
    <div class="row">
        <div class="col-12">
            <BlogPost v-for="post in posts" 
            :key="post.id" 
            :title="post.title" 
            :id="post.id" 
            :body="post.body" 
            :colorText="post.colorText"
            @addFavoritePost="addFavoritePost" />
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

