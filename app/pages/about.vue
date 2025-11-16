<script setup>
const { data } = await useAsyncData('test', () =>
  $fetch('https://jsonplaceholder.typicodse.com/posts')
)
</script>

<template>
  <NuxtClientFallback fallback="Loading component...">
    <div>{{ data }}</div>
  </NuxtClientFallback>
</template>