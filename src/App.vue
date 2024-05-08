<script setup>

import NavBar from './components/NavBar.vue';
import CountriesList from './components/CountriesList.vue';
import CountryDetails from './components/CountryDetails.vue';

</script>

<template>
  <div class="app">
    <div class='content-wrap'>
      <NavBar></NavBar>
    
      <router-view></router-view>
    </div>
  </div>
</template>

<style>

html {
  display:flex; 
  justify-content: center;
}

header { 
  background-color:#f8f8f8;
  height:100px;
  display: flex;
  align-content: center;
  margin-bottom: 50px;
  position: fixed;
  top: 0px;
  z-index: 2;
  width: 100%;
}

header h1 {
  text-align: center;
}


.content-wrap {
  width: 100%;
    margin: 0 auto;
    position: relative;
    margin-top: 140px;
    display: flex; 
    justify-content:center
}

</style>