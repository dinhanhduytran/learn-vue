<script setup>
import EventCard from "../components/EventCard.vue"
import {ref, onMounted} from 'vue'
import EventService from "@/services/EventService"

const events = ref(null)

const fetchEvents = async () => {
  try {
    const res = await EventService.getEvents()
    events.value = res.data
  } catch (error) {
    console.log(error)
  }
}

onMounted(fetchEvents)


</script>

<template>
  <h1>Events For Good</h1> <!-- new element -->

  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>