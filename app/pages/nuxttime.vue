<template>
    <MainHeader/>
    <hr>
    <h1>Nuxt Date Time </h1>

    <!-- how to get nuxt time  -->
   <strong>get Date is  :  </strong>
   <!-- formating props  -->
    <NuxtTime :datetime="Date.now()" 
    month="long"
    day="2-digit"
    year="numeric"
    hour="2-digit"
    minute="2-digit"
    second="numeric"
    time-zone-name="long"

    />
    <br>
   

    <!-- the date and time value to dislpaly , you can provide  -->
</template>


 