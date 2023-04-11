<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">No employees</p>
    <table v-else>
      <thead>
        <tr>
          <th>Employee name</th>
          <th>Employee email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.defineComponent">
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.name" />
          </td>
          <td v-else>{{ employee.name }}</td>
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else>{{ employee.email }}</td>
          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)">Save</button>
            <button class="muted-button" @click="cancelEdit(employee)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(employee)">Edit</button>
            <button @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'EmployeeTable',
    props: {
      employees: Array,
    },
    data() {
      return {
        editing: null,
      }
    },
    methods: {
      editMode(employee) {
        this.cachedEmployee = Object.assign({}, employee)
        this.editing = employee.id
      },
      cancelEdit(employee) {
        Object.assign(employee, this.cachedEmployee)
        this.editing = null;
      },
      editEmployee(employee) {
        if (employee.name === '' || employee.email === '') 
          return this.$emit('edit:employee', employee.id, employee);
        
        this.editing = null
      }
    }
  }
</script>

<style scoped>
  table {
    margin: 0 0 1.5rem 0;
    border-collapse: collapse;
    border-spacing: 0;
    width: 100%;
    max-width: 100%;
  }

  thead th {
    border-bottom: 2px solid #dedede;
  }

  th, td {
    text-align: left;
    padding: 0.5rem;
  }

  td {
    border-bottom: 1px solid #dedede;
  }

  button {
    margin: 0 0.5rem 0 0;
  }

  button:last-child {
    margin-right: 0;
  }
</style>