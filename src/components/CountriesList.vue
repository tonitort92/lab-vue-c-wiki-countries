<script setup>
import { ref } from 'vue';

const countries = ref([]);

async function countriesToRender() {
    try {
        const response = await fetch("https://ih-countries-api.herokuapp.com/countries"); 
        countries.value = await response.json();
    } catch (error) { 
        console.log('No se pueden cargar los países:', error);
    }
}
countriesToRender();

</script>

<template>
    <div class = 'row' id='max-width'>
        <div class = 'col-3 '>
            <h2>Wiki Country List</h2>
            <ul id='list-of-countries' v-if="countries.length > 0">
                <li  v-for='(country, index) in countries' :key='index'>
                    <router-link :to="`/list/${country.alpha3Code}`">
                    <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="Flag of {{ country.name.common }}">
                        <h3>{{ country.name.common}}</h3>
                    </router-link>
                </li>
             </ul>
        </div>
        <router-view class='col-9'></router-view>
    </div>
</template>

<style>

header { background-color: #f8f8f8;}

#max-width{
        max-width:1440px;
        min-width:1440px;
    }

div .col-3 h2 { margin-bottom: 25px;
font-size: 20px; }

div .col-9 h2 { margin-bottom: 25px;
font-size: 20px; }

#list-of-countries{

  list-style:none; 
  text-decoration: none; 
  color: darkgray;
  display: flex; 
  justify-content: center;
  flex-direction: column;
  padding-left: 0;

}

div h3{

    font-size: 24;
    text-decoration:none;
    font-weight: 400;

}

li a {
    text-decoration:none;
    color: #404040;
    padding: 20px
}

#list-of-countries li{

  margin-bottom: 30px;
  background-color:#f8f8f8;
  display:flex; 
  flex-direction: column;
  justify-content: center;
  align-content:center;
  text-decoration:none;
  text-align:center;
  border-radius: 5px; 
  box-shadow: 0px 3px 15px rgba(0,0,0,0.1);
  border: solid 4px #EFEFEF;

}

#list-of-countries img {
    margin-bottom: 20px;
}




</style>
