<template>
  <div>
    <h1>Events</h1>
    <router-link :to="{ name: 'event-details', params: { id: 1 } }"
      >Show Event #1</router-link
    >
  </div>
</template>
