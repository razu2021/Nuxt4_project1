<script setup>
const { data } = await useAsyncData('test', () =>
  $fetch('https://jsonplaceholder.typicode.com/posts')
)
</script>

<template>
  <div>{{ data }}</div>
</template>