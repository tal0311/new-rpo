<template>
  <section class='activity-log'>
      <table>
        <tbody>
          <tr v-for="activity in activities" :key="activity.id">
              <td>{{activity.createdAt}}</td>
              <td>{{activity.byMember.fullname}}</td>
              <td>{{activity.txt}}</td>
          </tr>
        </tbody>
      </table>
  </section>
</template>

<script>
// import { carService } from '../services/car-service.js'
// import carFilter from '../components/car-filter.vue'

export default {
  name: 'activity-log',
  props: {
    activities: Array,
  },
  data() {
      return {
         
      };
  },
  methods: {

  },
  computed: {

  },
  created() {},
  components: {

  },
}
</script>