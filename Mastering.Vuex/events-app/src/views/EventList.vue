
<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
  </div>
</template>
<script>
import EventCard from '@/components/EventCard.vue';
import EventService from "@/services/EventService.js";

export default {
    components: {
        EventCard
    },
    data(){
      return {
        events: []
      }
    },
    created() {//see https://vuejs.org/v2/api/#created
      EventService.getEvents()
      .then(response => {
        console.log(response.data);
        this.events = response.data;
      })
      .catch(error => {
        console.log(error);
      })
    }
};
</script>