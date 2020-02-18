<template>
  <div id="app">
    <h1 class="app__title">Date Range Picker Filter</h1>
    <DatePicker v-model="range" lang="en" range type="month" format="MMMM/YYYY" rangeSeparator=" - "/>
    <TableComponent :dateRange="this.range"/>
  </div>
</template>

<script>
import DatePicker from "vue2-datepicker";
import 'vue2-datepicker/index.css';
import TableComponent from './components/TableComponent';

export default {
  name: 'App',
  components: {
    DatePicker,
    TableComponent
  },
  data() { 
    return {
      range: ''
    }
  }
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  text-align: center;
  align-items: center;
  margin-top: 5vh;
}
.app__title {
  margin-bottom: 8vh;
}
</style>
