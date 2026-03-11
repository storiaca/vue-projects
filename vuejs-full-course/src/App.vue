<script setup>
import Welcome from './components/pages/Welcome.vue';
import Layout from "./components/layouts/Layout.vue"
import Dashboard from "./components/pages/Dashboard.vue"
import Workout from "./components/pages/Workout.vue"

const selectDisplay = 3
</script>

<template>
  <Layout>
    <!-- PAGE 1 -->
    <Welcome v-if="selectDisplay == 1"/>
    <!-- PAGE 2 -->
    <Dashboard v-if="selectDisplay == 2"/>
    <!-- PAGE 3 -->
    <Workout v-if="selectDisplay == 3"/>
  </Layout>
</template>

<style scoped>

</style>
