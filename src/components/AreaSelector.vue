<!-- AreaSelector.vue -->
<template>
    <div>
        <label for="area-select">Select an area:</label>
        <select v-if="areas" id="area-select" v-model="selectedArea" @change="onAreaChange">
            <option disabled value="">Please select an area</option>
            <option v-for="area in areas" :key="area.isoCode" :value="area.name">{{ area.name }}</option>
        </select>
    </div>
</template>
  
<script>
export default {
    props: ["countryIsoCode"],
    data() {
        return {
            areas: null,
            selectedArea: "",
        };
    },
    created() {
        if (this.countryIsoCode) {
            this.fetchAreas();
        }
    },
    methods: {
        fetchAreas() {
            console.log("Fetching areas for country:", this.countryIsoCode);
            this.$http
                .get(`https://wft-geo-db.p.rapidapi.com/v1/geo/countries/${this.countryIsoCode}/regions`, {
                    headers: {
                        "X-RapidAPI-Host": "wft-geo-db.p.rapidapi.com",
                        "X-RapidAPI-Key": "0d26327d82msh32aef66c29a4f2bp1e8a47jsne7d5a523895b",
                    },
                })
                .then((response) => {
                    this.areas = response.data.data;
                })
                .catch((error) => {
                    console.error("Error fetching area data:", error);
                });
        },
        onAreaChange() {
            this.$emit("area-selected", this.selectedArea);
            
        },
    },
    watch: {
        countryIsoCode: function (newVal, oldVal) {
            console.log("Received country code:", newVal);
            if (newVal !== oldVal) {
                this.fetchAreas();
            }
        },
    },
};

</script>
  