<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'
const event = ref(null)


const props = defineProps({
    id: {
        required: true,
        type: [String, Number]
    }
})

const fetchEvent = async() => {
    try {
        const res = await EventService.getEvent(props.id)
        event.value = res.data
    } catch (error) {
        console.log(error)
    }
}

onMounted(fetchEvent)
</script>

<template>
    <div v-if="event">
      <h1>{{ event.title }}</h1>
      <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
      <p>{{ event.description }}</p>
    </div>
    <div v-else>
      <p>Loading event...</p>
    </div>
  </template>