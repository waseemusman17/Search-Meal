<template lang="">
    <div class="flex flex-col p-8 ">
        <input 
            type="text" 
            placeholder="Search for Meals" 
            class="rounded border-2 border-gray-200 w-full"
        />

        <div class="flex justify-center gap-1 mt-2">
            <router-link :to="{name:'byLetter', params:{ letter }}" v-for="letter of letters" :key="letter">
                {{ letter }}
            </router-link>
        </div>

        <pre>{{ ingredients }}</pre>

    </div>
</template>

<script setup>
    import { computed, onMounted, ref } from 'vue';
    import store from '../store';
    import axiosClient from '../axiosClient.js'

    const letters = 'ABCDEFGHIJKLMNOPQRESTUVWXYZ'.split('');
    const ingredients = ref([])

    onMounted(async () => {
        const response = await axiosClient.get('/list.php?i=list')
        console.log(response.data);
        ingredients.value = response.data;
    });

</script>

<style lang="">
    
</style>