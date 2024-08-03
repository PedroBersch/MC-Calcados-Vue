<script>
export default {
  data() {
    return {
      name: "Bersch",
      status: "active",
      tasks: ["one", "two", "three"],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status == "active") {
        this.status = "pending";
      } else if (this.status == "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is inactive</p>
  <p v-else>Nenhum dos dosi</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <a :href="link">google.com</a>

  <button @click="toggleStatus">Change status</button>
</template>
