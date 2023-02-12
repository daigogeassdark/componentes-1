<script setup>
import { ref } from 'vue'
//defineProps([ 'id', 'title', 'body' , 'colorText'])
//se le puede pasar string, number, boolean, array, object, symbol
defineProps({
    id: {
        type: String,
        required: true
    },
    title: {
        type: String,
        required: true
    },
    body: {
        type: String,
        required: true,
        default: 'Sin descripcion'
    },
    colorText: {
        type: String,
        required: true
    }
    
})

const emit = defineEmits(['addFavoritePost'])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`" > {{ id }} {{title}}:</h5>
            <p>
                {{body}}
            </p>
            <button class="btn btn-outline-primary" @click="emit('addFavoritePost', title)">Add to Favorite Post</button>
        </div>

    </div>
</template>