<script setup>
import { ref, onMounted, watch } from 'vue';
import { useRoute } from 'vue-router';

const countries = ref([]);
const country = ref(null);
const route = useRoute();

async function fetchCountries() {
    try {
        const response = await fetch("https://ih-countries-api.herokuapp.com/countries");
        countries.value = await response.json();
    } catch (error) {
        console.error('Error al cargar los países:', error);
    }
}

function selectCountryDetails(alpha3Code) {
    country.value = countries.value.find(c => c.alpha3Code === alpha3Code);
}

onMounted(async () => {
  await fetchCountries();
  selectCountryDetails(route.params.alpha3Code);
});

watch(() => route.params.alpha3Code, (newAlpha3Code) => {
  if (newAlpha3Code && countries.value.length) {
    selectCountryDetails(newAlpha3Code);
  }
}, { immediate: true });
</script>

<template>
        <div class = col-9>
            <h2>Wiki Country Details</h2>
                <div v-if="country">
                    <p>Common Country Name: {{ country.name.common }}</p>
                    <p>Official Country Name: {{ country.name.official }}</p>
                    <p>Official Native Country Name: {{ country.name?.native?.eng?.official }}</p>
                    <p>Common Native Country Name: {{ country.name?.native?.eng?.common }}</p>
                    <p>Top-Level Domain (TLD): {{ country.tld ? country.tld[0] : 'No TLD available' }}</p>
                    <p>Alpha 2 Code: {{ country.alpha2Code }}</p>
                    <p>Alpha 3 Code: {{ country.alpha3Code }}</p>
                    <p v-show="country.independent">Is an Independent Country</p>
                    <p v-show="!country.independent">Is not an Independent Country</p>
                    <p v-show="country.status === 'officially-assigned'">Is officially recognized</p>
                    <p v-show="country.status !== 'officially-assigned'">Is not officially recognized</p>
                    <p v-if="country.unMember">Is part of the UN</p>
                    <p v-if="!country.unMember">Is not part of the UN</p>
                    <p v-if="country.currencies?.XCD">
                    The official currency of the country is {{ country.currencies.XCD.name }} and its symbol is {{ country.currencies.XCD.symbol }}
                    </p>
                    <p v-else>No official currency information available</p>
                    <p>The country prefix and suffix extensions for dialing phone are {{ country.idd?.root }}{{ country.idd?.suffixes ? ' - ' + country.idd.suffixes.join(', ') : '' }}</p>
                    <p>The capital city is {{ country.capital }}</p>
                    <p>The shorthand for the country is {{ country.altSpellings }}</p>
                    <p>The region of the country is {{ country.region }}</p>
                    <p>The subregion of the country is {{ country.subregion }}</p>
                    <p>The subregion of the country is {{ country.languages }}</p>
                    <p >The country translations are:
                       <span v-for="(translation, language) in country.translations" :key="language">
  {{ language }} - Oficial: {{ translation.official }}, Común: {{ translation.common }}
</span></p>

                    <p>The coordinates of the country are {{ country.latlng }}</p>
                    <p v-if='country.landlocked'>The country is landlocked</p>
                    <p v-if='!country.landlocked'>The country is not landlocked</p>
                    <p v-if='country.borders'>The borders are {{country.borders}}</p>
                    <p v-if='!country.borders'>There are no borders</p>
                    <p v-if='country.area'>The country area is {{ country.area }} square kilometres</p>
                    <p v-if='country.demonyms'>The country denomyns are {{ country.demonyms }}</p>
                </div>
            </div>

    </template>

<style>

    div .col-9 {
        padding-left: 30px
    }



</style>

"name": {
    "common": "Antigua and Barbuda",
    "official": "Antigua and Barbuda",
    "native": {
      "eng": {
        "official": "Antigua and Barbuda",
        "common": "Antigua and Barbuda"
      }
    }
  },
  "tld": [".ag"],
  "alpha2Code": "AG",
  "alpha3Code": "ATG",
  "independent": true,
  "status": "officially-assigned",
  "unMember": true,
  "currencies": {
    "XCD": {
      "name": "Eastern Caribbean dollar",
      "symbol": "$"
    }
  },
  "idd": {
    "root": "+1",
    "suffixes": ["268"]
  },
  "capital": ["Saint John's"],
  "altSpellings": ["AG"],
  "region": "Americas",
  "subregion": "Caribbean",
  "languages": {
    "eng": "English"
  },
  "translations": {
    "ces": {
      "official": "Antigua a Barbuda",
      "common": "Antigua a Barbuda"
    },
    "cym": {
      "official": "Antigwa a Barbiwda",
      "common": "Antigwa a Barbiwda"
    },
    "deu": {
      "official": "Antigua und Barbuda",
      "common": "Antigua und Barbuda"
    },
    "est": {
      "official": "Antigua ja Barbuda",
      "common": "Antigua ja Barbuda"
    },
    "fin": {
      "official": "Antigua ja Barbuda",
      "common": "Antigua ja Barbuda"
    },
    "fra": {
      "official": "Antigua -et-Barbuda",
      "common": "Antigua-et-Barbuda"
    },
    "hrv": {
      "official": "Antigva i Barbuda",
      "common": "Antigva i Barbuda"
    },
    "hun": {
      "official": "Antigua \u00e9s Barbuda",
      "common": "Antigua \u00e9s Barbuda"
    },
    "ita": {
      "official": "Antigua e Barbuda",
      "common": "Antigua e Barbuda"
    },
    "jpn": {
      "official": "\u30a2\u30f3\u30c1\u30b0\u30a2\u30d0\u30fc\u30d6\u30fc\u30c0",
      "common": "\u30a2\u30f3\u30c6\u30a3\u30b0\u30a2\u30fb\u30d0\u30fc\u30d6\u30fc\u30c0"
    },
    "kor": {
      "official": "\uc564\ud2f0\uac00 \ubc14\ubd80\ub2e4",
      "common": "\uc564\ud2f0\uac00 \ubc14\ubd80\ub2e4"
    },
    "nld": {
      "official": "Antigua en Barbuda",
      "common": "Antigua en Barbuda"
    },
    "per": {
      "official": "\u0622\u0646\u062a\u06cc\u06af\u0648\u0627 \u0648 \u0628\u0627\u0631\u0628\u0648\u062f\u0627",
      "common": "\u0622\u0646\u062a\u06cc\u06af\u0648\u0627 \u0648 \u0628\u0627\u0631\u0628\u0648\u062f\u0627"
    },
    "pol": {
      "official": "Antigua i Barbuda",
      "common": "Antigua i Barbuda"
    },
    "por": {
      "official": "Antigua e Barbuda",
      "common": "Ant\u00edgua e Barbuda"
    },
    "rus": {
      "official": "\u0410\u043d\u0442\u0438\u0433\u0443\u0430 \u0438 \u0411\u0430\u0440\u0431\u0443\u0434\u0430",
      "common": "\u0410\u043d\u0442\u0438\u0433\u0443\u0430 \u0438 \u0411\u0430\u0440\u0431\u0443\u0434\u0430"
    },
    "slk": {
      "official": "Antigua a Barbuda",
      "common": "Antigua a Barbuda"
    },
    "spa": {
      "official": "Antigua y Barbuda",
      "common": "Antigua y Barbuda"
    },
    "swe": {
      "official": "Antigua och Barbuda",
      "common": "Antigua och Barbuda"
    },
    "urd": {
      "official": "\u0627\u06cc\u0646\u0679\u06cc\u06af\u0648\u0627 \u0648 \u0628\u0627\u0631\u0628\u0648\u0688\u0627",
      "common": "\u0627\u06cc\u0646\u0679\u06cc\u06af\u0648\u0627 \u0648 \u0628\u0627\u0631\u0628\u0648\u0688\u0627"
    },
    "zho": {
      "official": "\u5b89\u63d0\u74dc\u548c\u5df4\u5e03\u8fbe",
      "common": "\u5b89\u63d0\u74dc\u548c\u5df4\u5e03\u8fbe"
    }
  },
  "latlng": [17.05, -61.8],
  "landlocked": false,
  "borders": [],
  "area": 442,
  "demonyms": {
    "eng": {
      "f": "Antiguan, Barbudan",
      "m": "Antiguan, Barbudan"
    },
    "fra": {
      "f": "Antiguaise et barbudienne",
      "m": "Antiguaise et barbudien"
    }
  }