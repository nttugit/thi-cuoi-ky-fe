<!-- TodoList.vue -->
<template>
  <div>
    <h2>Danh sách điểm đặt biển quảng cáo</h2>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Address</th>
          <th scope="col">Type</th>
          <th scope="col">Format</th>
          <th scope="col">Ward</th>
          <th scope="col">Thao tác</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in spaces" :key="index">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ item.address }}</td>
          <td>{{ item.type }}</td>
          <td>
            {{ item.format }}
          </td>
          <td>{{ item.ward }}</td>
          <td>
            <button
              type="button"
              class="btn btn-info"
              @click="viewSurfaces(item.id)"
            >
              View surfaces
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      spaces: [],
    };
  },
  mounted() {
    this.loadSpaces();
  },
  methods: {
    async loadSpaces() {
      try {
        const response = await fetch("http://localhost:3000/spaces");
        const data = await response.json();
        this.spaces = data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },

    async viewSurfaces(spaceId) {
      this.$router.push(`/surfaces/space/${spaceId}`);
    },
  },
};
</script>

<style scoped>
/* Add any custom styles here */
</style>
