<template>

  <table class="table" v-if="dateRange != '' && dateRange != null">
    <thead class="thead-dark">
      <th>Client</th>
      <th>Due Date</th>
    </thead>
    <tbody>
      <tr v-for="(client, index) in filteredClients()" :key="index">
        <td v-for="(prop, key) in client" :key="key">{{ prop }}</td>
      </tr>
    </tbody>
  </table>

    <table class="table" v-else>
    <thead class="thead-dark">
      <th>Client</th>
      <th>Due Date</th>
    </thead>
    <tbody>
      <tr v-for="(client, index) in this.allClients" :key="index">
        <td v-for="(prop, key) in client" :key="key">{{ prop }}</td>
      </tr>
    </tbody>
  </table>

</template>

<script>
import Clients from '../Mock/clients';

export default {
  name: 'TableComponent',
  data() {
    return {
      allClients: []
    }
  },
  mounted() {
    this.allClients = Clients;
  },
  props: ['dateRange'],
  methods: {
      filteredClients() {
        return this.allClients.filter((client) => {
          let dueMonthOK = false;
          let dueYearOK = false;

          // months
          let months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
          let dueMonthIndex = months.indexOf(client.dueDate.substring(0, 3));
          let initialMonthIndex = this.dateRange[0].getMonth();
          let finalMonthIndex = this.dateRange[1].getMonth();

          // year
          let dueYear = client.dueDate.split('/')[1];
          let initialYear = this.dateRange[0].getFullYear();
          let finalYear = this.dateRange[1].getFullYear();

          // checking if dueMonth is between initial and final filtered months
          if (dueYear < finalYear) {
            dueMonthOK = (dueMonthIndex >= initialMonthIndex);
          } else if (dueYear == finalYear) {
            dueMonthOK = (dueMonthIndex <= finalMonthIndex);
          }

          // checking if dueYear is between initial and final filtered years
          dueYearOK = (dueYear >= initialYear && dueYear <= finalYear);

          return dueMonthOK && dueYearOK;
        })
      }
    }
  }
</script>

<style>
.table {
  width: 40%;
  margin-top: 5vh
}
</style>
