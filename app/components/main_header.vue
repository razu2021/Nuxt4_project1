<template>
    <div class="main_menu">
        <ul>
            <li><NuxtLink to="/">Home</NuxtLink></li>
            <li><NuxtLink to="/about">about</NuxtLink></li>
            <li><NuxtLink to="/nuxttime">Nuxt time</NuxtLink></li>
            <li><NuxtLink to="/route-fullpath">Route Fullpath</NuxtLink></li>
            <li><NuxtLink to="">Home</NuxtLink></li>
        </ul>
    </div>
</template>


<style scoped>
ul,li{
    list-style-type: none;
}
.main_menu{
    background-color: red;
}
.main_menu ul li{
   display: inline-block;
   padding: 10px 10px;
}

</style>