<script setup>
import { ref } from 'vue';
import Welcome from './components/pages/Welcome.vue';
import Layout from "./components/layouts/Layout.vue"
import Dashboard from "./components/pages/Dashboard.vue"
import Workout from "./components/pages/Workout.vue"
import { workoutProgram } from './utils';

const defaultData = {}
for(let workoutIdx in workoutProgram) {
  const workoutData = workoutProgram[workoutIdx]
  // create a for loop where we iterate over every workout
  defaultData[workoutIdx] = {} // initiakize the workout data obj

  // nested loop to loop over every exercise within a workout, and initialize it's input value to an empty string
  for(let e of workoutData.workout) {
    defaultData[workoutIdx][e.name] = ''
  }
}

const selectDisplay = ref(1)
const data = ref(defaultData) // {1...30: {exercise_name: "", ....}}
const selectedWorkout = ref(-1)


function handleChangeDisplay(idx) {
  selectDisplay.value = idx
}

function handleSelectWorkout(idx) {
  selectDisplay.value = 3
  selectedWorkout.value = idx
}

function handleSaveWorkout() {
  // save the current data snapshot to localstorage so we can retrive it next time
  localStorage.setItem('workouts', JSON.stringify(data.value))
  // show the dashboard
  selectDisplay.value = 2
  // deselect workout
  selectDisplay.value = -1
}
</script>

<template>
  <Layout>
    <!-- PAGE 1 -->
    <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectDisplay == 1"/>
    <!-- PAGE 2 -->
    <Dashboard :handleSelectWorkout="handleSelectWorkout" v-if="selectDisplay == 2"/>
    <!-- PAGE 3 -->
    <Workout :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
  </Layout>
</template>

<style scoped>

</style>
