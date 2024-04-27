<template>
  <div>
    <div id="superset-container"></div>
  </div>
</template>

<script>
import axios from 'axios';
const BACKEND_URL = process.env.DASHBOARD_ID;
const SUPERSET_URL = process.env.SUPERSET_URL;

export default {
  name: 'SupersetDashboard',
  props: {
    dashboardId: String,
  },
  methods: {
    async fetchGuestTokenFromBackend(dashboardId) {
      try {
        const url = `${BACKEND_URL}/api/guestToken?dashboardId=${dashboardId}`
        const response = await axios.get(url);
        const { guestToken } = response.data
        return guestToken
      } catch (error) {
        console.error('Error fetching dashboard data:', error);
      }
    }
  },
  mounted() {
    window.supersetEmbeddedSdk.embedDashboard({
      id: this.dashboardId,
      supersetDomain: SUPERSET_URL,
      mountPoint: document.getElementById("superset-container"),
      fetchGuestToken: () => this.fetchGuestTokenFromBackend(this.dashboardId),
      dashboardUiConfig: {
          hideTitle: true,
          filters: {
              expanded: true,
          },
          urlParams: {}
      },
    });
  }
}
</script>

<style>

#superset-container iframe {
  width: 100%;
  height: calc(100vh - 70px);
  border: 1px solid #ccc;
}
</style>
