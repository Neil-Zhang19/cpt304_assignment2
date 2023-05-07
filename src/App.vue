<template>
  <div>
    <CountrySelector @country-selected="selectedCountry = $event" />
    <AreaSelector :countryIsoCode="selectedCountry" @area-selected="onAreaSelected" /> 
    <PublicHolidaySelector v-if="selectedCountry" :country="selectedCountry" @holiday-selected="selectHoliday" />
    <WeatherInfo v-if="selectedCountry && selectedArea && selectedHoliday" :country= "selectedCountry" :area="selectedArea" :date="selectedHoliday.date" />
    <AccommodationInfo v-if="selectedArea && selectedHoliday" :area="selectedArea" :date="selectedHoliday.date" />
  </div>
</template>

<script>
import CountrySelector from "./components/CountrySelector.vue";
import AreaSelector from "./components/AreaSelector.vue";
import PublicHolidaySelector from "./components/PublicHolidaySelector.vue";
import WeatherInfo from "./components/WeatherInfo.vue";
import AccommodationInfo from "./components/AccommodationInfo.vue";

export default {
  components: {
    CountrySelector,
    AreaSelector,
    PublicHolidaySelector,
    WeatherInfo,
    AccommodationInfo,
  },
  data() {
    return {
      selectedCountry: "", 
      selectedArea: "",
      selectedHoliday: null,
    };
  },
  methods: {
    selectHoliday(holiday) {
      this.selectedHoliday = holiday;
      
    },
    onAreaSelected(area) {
      this.selectedArea = area;
    },
    
  },
};
</script>
