<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form/>
    <employee-table v-bind:employees="employees"/>
  </div>
</template>

<script>
import EmployeeForm from '@/components/EmployeeForm.vue'
import EmployeeTable from '@/components/EmployeeTable.vue'

export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: 'Richard Hendrix',
          email: 'bbalc@gmail.com'
        },
        {
          id: 2,
          name: 'Brian Balconi',
          email: 'fake@fake.com',
        },
        {
          id: 3,
          name: 'Ruby Balconi',
          email: 'noemail@dog.com'
        }
      ]
    }
  }
}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>