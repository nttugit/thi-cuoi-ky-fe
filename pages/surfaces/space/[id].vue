<!-- TodoList.vue -->
<template>
  <div>
    <h2>Danh sách điểm đặt biển quảng cáo</h2>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Format</th>
          <th scope="col">Size</th>
          <th scope="col">Amount</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in surfaces" :key="index">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ item.format }}</td>
          <td>{{ item.width }}m x {{ item.height }}m</td>
          <td>
            <button
              type="button"
              class="btn btn-info"
              @click="viewReports(item.id)"
            >
              Report
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <button type="button" class="btn btn-info" @click="backToSpaces()">
      Back
    </button>
  </div>
</template>

<script>
import { useRoute } from "vue-router";

export default {
  data() {
    return {
      surfaces: [],
    };
  },
  mounted() {
    this.loadSurfaces();
  },
  methods: {
    async loadSurfaces() {
      try {
        const route = useRoute();
        const spaceId = route.params.id;
        const response = await fetch(
          `http://localhost:3000/surfaces/space/${spaceId}`
        );
        const data = await response.json();
        this.surfaces = data;
        console.log("data", data);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },

    async viewReports(surfaceId) {
      this.$router.push(`/reports/surface/${surfaceId}`);
    },

    async backToSpaces() {
      this.$router.push(`/spaces`);
    },
  },
};
</script>

<style scoped>
/* Add any custom styles here */
</style>
