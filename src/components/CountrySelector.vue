<!-- CountrySelector.vue -->
<template>
    <div>
        <label for="country">Country:</label>
        <select id="country" v-model="selectedCountry" @change="onCountryChange">
            <option value="">Select a country</option>
            <option v-for="country in countries" :key="country.code" :value="country.code">
                {{ country.name }}
            </option>
        </select>
    </div>
</template>
  
<script>
import axios from 'axios';
export default {
    data() {
        return {
            countries: [],
            selectedCountry: "",
        };
    },
    created() {
        // this.$http
        axios.get("https://restcountries.com/v3.1/all")
            .then((response) => {
                this.countries = response.data.map((country) => ({
                    name: country.name.common,
                    code: country.cca2,
                }));
                if (this.countries.length > 0) {
                    this.selectedCountry = this.countries[0].code;
                    console.log("Selected country:", this.selectedCountry);
                    this.$emit("country-selected", this.selectedCountry);
                }
            })
            .catch((error) => {
                console.error("Error fetching country data:", error);
            });
    },
    methods: {
        onCountryChange() {
            console.log("Selected country:", this.selectedCountry);
            this.$emit("country-selected", this.selectedCountry);
        },
    },

};
</script>
  