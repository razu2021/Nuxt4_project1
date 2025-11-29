<script setup>

const route = useRoute()


const { data } = await useAsyncData('test', () =>
  $fetch('https://jsonplaceholder.typicode.com/posts')
)





</script>

<template>
  <MainHeader/>
 
  <h1>{{ route }}</h1>


<router-link to="{{ route.path }}">open link </router-link>
</template>