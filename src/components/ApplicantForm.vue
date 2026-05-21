<template>
  <div class="form-container">
    <h2>Submit Your Application</h2>
    
    <div v-if="successMessage" class="success-alert">
      {{ successMessage }}
    </div>

    <form @submit.prevent="handleSubmit" class="app-form">
      <div class="form-row">
        <div class="form-group">
          <label>Firstname</label>
          <input type="text" v-model="formData.firstname" required placeholder>
        </div> 
        <div class="form-group">
          <label>Surname</label>
          <input type="text" v-model="formData.surname" required placeholder>
        </div>
      </div>

      <div class="form-group">
        <label>Date of Birth (DOB)</label>
        <input type="date" v-model="formData.dob" required>
      </div>

      <div class="form-group">
        <label>Address</label>
        <textarea v-model="formData.address" required rows="3" placeholder></textarea>
      </div>

      <div class="form-group">
        <label>Phone Number</label>
        <input type="tel" v-model="formData.phone" required placeholder>
      </div>

      <div class="form-group">
        <label>Gender</label>
        <div class="radio-options">
          <label><input type="radio" v-model="formData.gender" value="Male" required> Male</label>
          <label><input type="radio" v-model="formData.gender" value="Female"> Female</label>
          <label><input type="radio" v-model="formData.gender" value="Other"> Other</label>
        </div>
      </div>

      <div class="form-group">
        <label>National ID</label>
        <input type="text" v-model="formData.nationalId" required>
      </div>

      <button type="submit" class="btn-submit">Submit Application</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-application'])
const successMessage = ref('')

const formData = ref({
  firstname: '', surname: '', dob: '', address: '', phone: '', gender: '', nationalId: ''
})

const handleSubmit = () => {
  emit('add-application', { ...formData.value })
  successMessage.value = 'Application submitted successfully! Check Admin Dashboard Tab.'
  
  // Guhanagura fomu
  formData.value = {
    firstname: '', surname: '', dob: '', address: '', phone: '', gender: '', nationalId: ''
  }
  setTimeout(() => { successMessage.value = '' }, 4000)
}
</script>

<style scoped>
.form-container { background: white; padding: 30px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); text-align: left; }
h2 { color: #2c3e50; margin-bottom: 20px; padding-bottom: 10px; border-bottom: 2px solid #eee; }
.app-form { display: flex; flex-direction: column; gap: 15px; }
.form-row { display: flex; gap: 15px; }
.form-row .form-group { flex: 1; }
.form-group { display: flex; flex-direction: column; gap: 5px; }
label { font-weight: bold; color: black; }
input[type="text"], input[type="date"], input[type="tel"], textarea {
  padding: 10px; border: 1px solid #ccc; border-radius: 4px; font-size: 15px;
}
.radio-options { display: flex; gap: 20px; padding: 5px 0; }
.radio-options label { font-weight: normal; cursor: pointer; }
.btn-submit { background-color: #27ae60; color: white; padding: 12px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 16px; }
.btn-submit:hover { background-color: #219653; }
.success-alert { background-color: #d4edda; color: #155724; padding: 12px; border-radius: 4px; margin-bottom: 15px; border: 1px solid #c3e6cb; }
</style>