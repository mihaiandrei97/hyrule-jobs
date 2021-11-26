<template>
  <div class="app">
    <header>
      <button @click="handleClick('title')">order by title</button>
      <button @click="handleClick('salary')">order by salary</button>
      <button @click="handleClick('location')">order by location</button>
    </header>
    <JobsList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import JobsList from "./components/JobsList.vue";
import Job from "./types/job";
import { OrderTerm } from "./types/OrderTerm";

export default defineComponent({
  name: "App",
  components: { JobsList },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: "Job 1",
        location: "Location 1",
        salary: 30000,
        id: "1",
      },
      {
        title: "Job 2",
        location: "Location 2",
        salary: 200,
        id: "2",
      },
      {
        title: "Job 3",
        location: "Location 3",
        salary: 220,
        id: "3",
      },
    ]);

    const order = ref<OrderTerm>("title");

    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return {
      jobs,
      handleClick,
      order,
    };
  },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;0,600;1,700&display=swap");

body {
  background: #f8b569;
  font-family: "Poppins", sans-serif;
}

header {
  display: flex;
  justify-content: center;
  gap: 20px;
}

header button {
  padding: 16px 24px;
  background: #f8f8f8;
  background: rgba(164, 240, 164, 0.671);
  border: 2px solid green;
  border-radius: 4px;
  cursor: pointer;
}

header button:hover {
  opacity: 0.9;
}
</style>
