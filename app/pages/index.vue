<script setup>
const { data } = await useAsyncData('test', () =>
  $fetch('https://jsonplaceholder.typicode.com/posts')
)

const users = ref({
  name:"md razu hossain raj",
  age:25 
})


</script>

<template>
  <div>
    <h1>Md Razu Hossain Raj </h1>
      <NuxtLink to="/about"> About page</NuxtLink>
     
  </div>
  
 
      <h1>{{ users.name }}</h1>
      <h1>{{ users.age }}</h1>

 <NuxtImg src="/1.jpg" />

</template>