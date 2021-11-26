<template>
  <div class="jobs-list">
    <p class="order">
      Ordered by <span>{{ order }}</span>
    </p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <p>{{ job.salary }}$</p>
          <div class="description">
            <p>
              Lorem ipsum dolor sit, amet consectetur adipisicing elit. Earum
              quidem perspiciatis explicabo nostrum consectetur libero numquam
              at iure minus. Veritatis, ut obcaecati. Vel explicabo aliquid
              quibusdam assumenda, expedita dignissimos sed.
            </p>
          </div>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import Job from "@/types/job";
import { OrderTerm } from "@/types/OrderTerm";
import { computed, defineComponent, PropType } from "vue";
export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
      default: () => [],
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });
    return { orderedJobs };
  },
});
</script>

<style scoped>
.jobs-list {
  width: 960px;
  margin: 48px auto;
}

.jobs-list ul {
  list-style-type: none;
}

.jobs-list ul li {
  background: white;
  padding: 16px 24px;
  margin-bottom: 16px;
  border-radius: 10px;
  text-align: justify;
}

.jobs-list ul li h2 {
  color: black;
  font-size: 2rem;
}

.jobs-list .salary p {
  font-size: 1rem;
  color: green;
  font-weight: 600;
}

.jobs-list .salary .description p {
  font-weight: 500;
  color: black;
}

.jobs-list .order {
  font-size: 1.4rem;
  text-align: center;
}

.jobs-list .order span {
  font-weight: 500;
  color: green;
}

.list-move {
  transition: all 1s;
}
</style>
