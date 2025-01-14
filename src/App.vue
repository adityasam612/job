<template>
  <div class="app">
    <button @click="handleClick('location')">Order by location</button>
    <button @click="handleClick('title')">Order by title</button>
    <button @click="handleClick('paycheck')">Order by paycheck</button>
    <job-list :jobs="jobs" :order="order"></job-list>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JOB from './assets/job'; 
import jobList from './components/jobList.vue';
import OrderTerm from './assets/order';

export default defineComponent({
  name: 'App',
  components: { jobList },
  setup() {
    const jobs = ref<JOB[]>([
      { title: 'professor', location: 'Rome', paycheck: 3500, id: '1', description: 'A scholar who passionately engages in teaching and research within their field of expertise. Professors inspire and mentor students, contributing significantly to academic advancement and knowledge dissemination.' },
      { title: 'nurse', location: 'Milan', paycheck: 1800, id: '2', description: 'A compassionate healthcare professional dedicated to patient care. Nurses provide essential medical support, administer treatments, and offer emotional comfort, ensuring the well-being of those in their care.' },
      { title: 'Driver', location: 'Turin', paycheck: 1300, id: '3', description: 'A skilled individual who operates vehicles to transport passengers or goods. Drivers are responsible for ensuring safe and efficient travel, often navigating complex routes and managing schedules.' },
      { title: 'Chef', location: 'Naples', paycheck: 2500, id: '4', description: 'A culinary artist who crafts delicious and visually appealing dishes. Chefs oversee kitchen operations, develop menus, and experiment with flavors to create memorable dining experiences.' },
      { title: 'Editor', location: 'remote', paycheck: 1250, id: '5', description: 'A meticulous wordsmith who refines and enhances written content. Editors review, revise, and perfect articles, books, and other texts, ensuring clarity, coherence, and accuracy in communication.' }
    ]);
    
    const order = ref<OrderTerm>('title');

    const handleClick = (term: OrderTerm) => {
      order.value = term;
      
      jobs.value.sort((a, b) => {
        if (term === 'paycheck') {
          return b.paycheck - a.paycheck;
        } else {
          return a[term].localeCompare(b[term]);
        }
      });
    };

    return { jobs, order, handleClick };
  }
});
</script>

<style scoped>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

button {
  margin: 10px 5px;
  padding: 10px 20px;
  font-size: 1em;
  color: #fff;
  background-color: #009688;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #00796b;
}

.job-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.job-item {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  transition: transform 0.2s;
}

.job-item:hover {
  transform: scale(1.02);
}

.job-title {
  font-size: 1.5em;
  margin-bottom: 5px;
  color: #333;
}

.job-location {
  font-size: 1.1em;
  color: #777;
}

.job-description {
  font-size: 1em;
  color: #555;
}

.job-paycheck {
  font-size: 1.2em;
  font-weight: bold;
  color: #009688;
}
</style>
