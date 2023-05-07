<!-- PublicHolidaySelector.vue -->
<template>
    <div>
      <label for="public-holiday">Public Holiday:</label>
      <select id="public-holiday" v-model="selectedHoliday" @change="$emit('holiday-selected', selectedHoliday)">
        <option value="">Select a public holiday</option>
        <option v-for="holiday in publicHolidays" :key="holiday.date" :value="holiday">
          {{ holiday.name }} - {{ holiday.date }}
        </option>
      </select>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      country: String,
    },
    data() {
      return {
        publicHolidays: [],
        selectedHoliday: null,
      };
    },
    watch: {
      country: {
        handler() {
          this.fetchPublicHolidays();
        },
      },
    },
    methods: {
      async fetchPublicHolidays() {
        if (!this.country) {
          return;
        }
  
        const options = {
          method: 'GET',
          url: `https://public-holiday.p.rapidapi.com/${new Date().getFullYear()}/${this.country}`,
          headers: {
            'X-RapidAPI-Key': '0d26327d82msh32aef66c29a4f2bp1e8a47jsne7d5a523895b',
            'X-RapidAPI-Host': 'public-holiday.p.rapidapi.com',
          },
        };
  
        try {
          const response = await axios.request(options);
          this.publicHolidays = response.data;
        } catch (error) {
          console.error(error);
        }
      },
    },
  };
  </script>
  