<template>
  <div id="app">
    <SupersetDashboard
      :dashboardId='dashboardId'
    />
  </div>
</template>

<script>
import SupersetDashboard from './components/SupersetDashboard.vue'
const DASHBOARD_ID = process.env.DASHBOARD_ID;

export default {
  name: 'App',
  components: {
    SupersetDashboard
  },
  data() {
    return {
      dashboardId: DASHBOARD_ID,
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
