<template>
  <div class="main-layout">
    <header class="app-header">
      <h1>Job Agency Portal</h1>
      <div class="nav-tabs">
        <button 
          :class="{ 'tab-btn': true, 'active': currentTab === 'form' }" 
          @click="currentTab = 'form'"
        >
          Applicant Form
        </button>
        <button 
          :class="{ 'tab-btn': true, 'active': currentTab === 'admin' }" 
          @click="currentTab = 'admin'"
        >
          Administrator Dashboard 
          <span class="count-badge" v-if="allApplications.length > 0">{{ allApplications.length }}</span>
        </button>
      </div>
    </header>

    <main class="app-content">
      <ApplicantForm 
        v-if="currentTab === 'form'" 
        @add-application="handleNewApplication" 
      />
      
      <AdminDashboard 
        v-if="currentTab === 'admin'" 
        :apps="allApplications" 
      />
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ApplicantForm from './components/ApplicantForm.vue'
import AdminDashboard from './components/AdminDashboard.vue'

const currentTab = ref('form')
const allApplications = ref([])

const handleNewApplication = (data) => {
  allApplications.value.push(data)
}
</script>

<style>
body { background-color: #f3f4f6; margin: 0; font-family: 'Segoe UI', system-ui, sans-serif; }
.main-layout { max-width: 1000px; margin: 40px auto; padding: 0 20px; }
.app-header { text-align: center; margin-bottom: 30px; }
.app-header h1 { color: #2c3e50; font-size: 32px; margin-bottom: 20px; }
.nav-tabs { display: flex; justify-content: center; gap: 10px; background: #e0e0e0; padding: 6px; border-radius: 8px; max-width: fit-content; margin: 0 auto; }
.tab-btn { padding: 12px 24px; border: none; background: transparent; font-size: 16px; font-weight: 600; color: #555; cursor: pointer; border-radius: 6px; transition: all 0.3s; }
.tab-btn.active { background: white; color: #27ae60; box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
.count-badge { background: #27ae60; color: white; padding: 2px 7px; border-radius: 10px; font-size: 12px; margin-left: 5px; }
.app-content { margin-top: 25px; }
</style>