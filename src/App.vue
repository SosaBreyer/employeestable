<script>
  import EmployeeForm from './components/EmployeeForm.vue'
  import EmployeeTable from './components/EmployeeTable.vue'

  export default {
    name: 'app',
    components: {
      EmployeeForm,
      EmployeeTable,
    },
    data() {
      return {
        employees: [
          {
            id: 1,
            name: 'Richard Hendricks',
            email: 'richard@piedpiper.com',
          },
          {
            id: 2,
            name: 'Bertram Gilfoyle',
            email: 'gilfoyle@piedpiper.com',
          },
          {
            id: 3,
            name: 'Dinesh Chugtai',
            email: 'dinesh@piedpiper.com',
          },
        ],
      }
    },
    methods: {
      addEmployee(employee) {
        const lastId =
          this.employees.length > 0
            ? this.employees[this.employees.length - 1].id
            : 0;
        const id = lastId + 1;
        const newEmployee = { ...employee, id };

        this.employees = [...this.employees, newEmployee];
      },
      deleteEmployee(id) {
        this.employees = this.employees.filter(
          employee => employee.id !== id
        )
      },
      editEmployee(id, updatedEmployee) {
        this.employees = this.employees.map(
          employee => employee.id === id 
            ? updatedEmployee 
            : employee
        )
      }
    }
  }
</script>

<template>
  <h1>Employees</h1>

  <EmployeeForm @add:employee="addEmployee" />
  <EmployeeTable 
    v-bind:employees="employees" 
    @delete:employee="deleteEmployee"
    @edit:employee="editEmployee"
  />
</template>

<style>
  button {
    display: inline-block;
    border-radius: 4px;
    background: #009435;
    border: 1px solid #009435;
    color: #ffffff;
    font-weight: 600;
    font-size: 1rem;
    text-transform: none;
    padding: 0.75rem 1.25rem;
    margin: 0 0 0.5rem 0;
    vertical-align: middle;
    text-align: center;
    cursor: pointer;
    text-decoration: none;
    line-height: 1;
  }

  button:hover {
    background: #32a95d;
    border: 1px solid #32a95d;
    color: #ffffff;
    text-decoration: none;
  }
</style>