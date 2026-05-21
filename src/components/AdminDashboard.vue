<template>
  <div class="dashboard-container">
    <h2>Submitted Applications Dashboard</h2>

    <div v-if="apps.length === 0" class="placeholder-msg">
      <p>No applications submitted yet. Please go to "Applicant Form" tab to add one.</p>
    </div>

    <div v-else class="table-responsive">
      <table class="data-table">
        <thead>
          <tr>
            <th>#</th>
            <th>Full Name</th>
            <th>DOB</th>
            <th>Gender</th>
            <th>Phone</th>
            <th>National ID</th>
            <th>Address</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(applicant, index) in apps" :key="index">
            <td>{{ index + 1 }}</td>
            <td class="font-bold">{{ applicant.firstname }} {{ applicant.surname }}</td>
            <td>{{ applicant.dob }}</td>
            <td>{{ applicant.gender }}</td>
            <td>{{ applicant.phone }}</td>
            <td>{{ applicant.nationalId }}</td>
            <td>{{ applicant.address }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
defineProps({
  apps: { type: Array, required: true }
})
</script>

<style scoped>
.dashboard-container { background-color:black; padding: 30px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); text-align: left; }
h2 { color: #2c3e50; margin-bottom: 20px; padding-bottom: 10px; border-bottom: 2px solid #eee; }
.placeholder-msg { text-align: center; padding: 40px; color: #7f8c8d; font-style: italic; }
.table-responsive { overflow-x: auto; }
.data-table { width: 100%; border-collapse: collapse; margin-top: 10px; }
.data-table th, .data-table td { padding: 12px; border-bottom: 1px solid #eee; text-align: left; }
.data-table th { background-color: #f8f9fa; color: #2c3e50; font-weight: 600; }
.font-bold { font-weight: 600; }
</style>