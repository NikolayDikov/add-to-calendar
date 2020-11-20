<template>
  <div id="app">
    <CalendarButtons
      :cinputJSON="inputJSON"
    />
  </div>
</template>

<script>
/* eslint no-undef: "warn" */
import CalendarButtons from './components/CalendarButtons.vue'

export default {
  name: 'App',
  components: {
    CalendarButtons
  },
  data() {
    return {
      inputJSON,
    };
  },
}
</script>

<style>
  .mrEdit{
    display: none !important;
  }
</style>
