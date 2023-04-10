<template>
    <!-- wrapper div de bootstrap -->
    <div class="container">
    <!-- row wrapper div de bootstrap -->
        <div class="row">
            <div class="col-5">
                <div class="list-group">
                <router-link
                    v-for="(country, index) in countries"
                    :key="index"
                    :to="`/list/${country.alpha3Code}`"
                    class="list-group-item list-group-item-action d-flex flex-column justify-content-center">
                <img class="flag" :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="">
                    <p>
                    {{ country.name.common }}
                    </p>
                </router-link>
                </div>
            </div>
            <div class="col-7">
                <router-view />
            </div>
        </div>
    </div>
</template>

<script>
    export default {
    name: "CountriesList",
    data() {
        return {
        countries: null,
        };
    },
    methods: {
        async fetchCountries() {
        const response = await fetch(
            "https://ih-countries-api.herokuapp.com/countries"
        );
        const finalResponse = await response.json();
        this.countries = finalResponse;
        },
    },
    created() {
        this.fetchCountries();
    },
    };
</script>

<style scoped>
.flag {
  width: 50px;
  height: auto;
}
</style>