<!-- AccommodationInfo.vue -->
<template>
    <div v-if="accommodations.length">
        <h3>Short-term Accommodation Rentals</h3>
        <ul>
            <li v-for="accommodation in accommodations" :key="accommodation.id">
                {{ accommodation.name }} - {{ accommodation.price }} per night
            </li>
        </ul>
    </div>
</template>
  
<script>
export default {
    props: {
        area: String,
        date: String,
    },
    data() {
        return {
            accommodations: [],
        };
    },
    watch: {
        area: {
            // eslint-disable-next-line no-unused-vars
            handler() {
                this.fetchAccommodationInfo();
            },
            immediate: true,
        },
        date: {
            // eslint-disable-next-line no-unused-vars
            handler() {
                this.fetchAccommodationInfo();
            },
            immediate: true,
        },
    },
    methods: {
        fetchAccommodationInfo() {
            
            if (!this.area || !this.date) {
                return;
            }

            // Fetch accommodation information for the selected area and date
            // Replace with actual API call here.
            this.accommodations = [
                { id: 1, name: 'Cozy Apartment', price: 100 },
                { id: 2, name: 'Modern Loft', price: 150 },
            ];
        },
    },
};
</script>
  