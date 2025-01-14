<template>
    <div class="job-list">
      <p>Order by {{ order }}</p>
      <transition-group name="list" tag="ul">
        <li v-for="job in jobs" :key="job.id">
          <h2>{{ job.title }} in {{ job.location }}</h2>
          <div>
            <p>{{ job.paycheck }} euros</p>
            <div>
              <p>{{ job.description }}</p>
            </div>
          </div>
        </li>
      </transition-group>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, PropType } from 'vue';
  import job from '@/assets/job';
  import OrderTerm from '@/assets/order';
  
  export default defineComponent({
    props: {
      jobs: {
        required: true,
        type: Array as PropType<job[]>
      },
      order: {
        required: true,
        type: String as PropType<OrderTerm>
      }
    }
  });
  </script>
  
  <style scoped>
 .list-move{
    transition: all 1s;
 }
  </style>
  