<template>
  <div class="flex min-h-screen bg-slate-50 font-sans text-slate-900">
    <!-- Sidebar -->
    <Sidebar />

    <!-- Main Content Area -->
    <div class="flex-1 flex flex-col ml-64 transition-all duration-300">

      <!-- Top Header -->
      <TopHeader />

      <!-- Page Content -->
      <main class="flex-1 p-8 overflow-y-auto">

        <div class="flex justify-between items-end mb-8">
          <div>
            <h1 class="text-2xl font-bold text-slate-900 tracking-tight">System Overview</h1>
            <p class="text-slate-500 mt-1">Monitor real-time sync status and inter-platform messaging queues.</p>
          </div>
          <div class="flex gap-3">
            <button
              class="px-4 py-2 bg-white border border-slate-200 text-slate-600 font-medium rounded-lg text-sm shadow-sm hover:bg-slate-50 transition">
              Download Report
            </button>
            <button @click="showModal = true"
              class="px-4 py-2 bg-indigo-600 text-white font-medium rounded-lg text-sm shadow-lg shadow-indigo-200 hover:bg-indigo-700 transition flex items-center gap-2">
              + New Dispatch
            </button>
          </div>
        </div>

        <!-- Metric Grid -->
        <StatGrid />

        <!-- Main Feed Layout -->
        <div class="grid grid-cols-1 xl:grid-cols-3 gap-8">

          <!-- Feed (Takes up 2 cols) -->
          <div class="xl:col-span-2">
            <ActivityFeed :messages="messages" />
          </div>

          <!-- Right Column: Analytics / Mini-widgets -->
          <div class="space-y-6">
            <!-- Chart Placeholder -->
            <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
              <h3 class="font-bold text-slate-800 mb-4">Message Volume</h3>
              <div class="h-40 flex items-end justify-between gap-2 px-2">
                <!-- Fake CSS Chart -->
                <div v-for="h in [40, 65, 30, 85, 50, 95, 60]" :key="h"
                  class="w-full bg-indigo-100 rounded-t hover:bg-indigo-500 transition-colors relative group"
                  :style="{ height: h + '%' }">
                  <div
                    class="absolute -top-8 left-1/2 -translate-x-1/2 bg-slate-800 text-white text-[10px] py-1 px-2 rounded opacity-0 group-hover:opacity-100 transition-opacity">
                    {{ h }}
                  </div>
                </div>
              </div>
              <div class="flex justify-between mt-3 text-xs text-slate-400 font-mono uppercase">
                <span>Mon</span><span>Tue</span><span>Wed</span><span>Thu</span><span>Fri</span><span>Sat</span><span>Sun</span>
              </div>
            </div>

            <!-- Health Check -->
            <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
              <h3 class="font-bold text-slate-800 mb-4">Node Health</h3>
              <div class="space-y-4">
                <div v-for="node in ['HRMS-01', 'LMS-Core', 'WMS-East']" :key="node"
                  class="flex items-center justify-between text-sm">
                  <span class="text-slate-600 font-medium">{{ node }}</span>
                  <div class="flex items-center gap-2">
                    <span class="w-16 h-1 bg-slate-100 rounded-full overflow-hidden">
                      <div class="h-full bg-emerald-500 w-[95%]"></div>
                    </span>
                    <span class="text-emerald-600 font-bold text-xs">OK</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

        </div>

      </main>
    </div>

    <!-- Dispatch Modal -->
    <div v-if="showModal" class="fixed inset-0 z-50 flex items-center justify-center p-4">
      <div class="absolute inset-0 bg-slate-900/60 backdrop-blur-sm transition-opacity" @click="showModal = false">
      </div>
      <div
        class="bg-white rounded-2xl shadow-2xl w-full max-w-lg relative z-10 overflow-hidden transform transition-all scale-100">

        <div class="px-6 py-4 border-b border-slate-100 flex justify-between items-center bg-slate-50/50">
          <h3 class="font-bold text-slate-800 text-lg">Broadcast Dispatch</h3>
          <button @click="showModal = false" class="text-slate-400 hover:text-rose-500 transition">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
              stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>

        <div class="p-8 space-y-6">
          <div>
            <label class="block text-xs font-bold uppercase text-slate-500 mb-2">Protocol Type</label>
            <div class="grid grid-cols-3 gap-3">
              <button
                class="border border-indigo-600 bg-indigo-50 text-indigo-700 font-bold text-xs py-2 rounded-lg">Standard</button>
              <button
                class="border border-slate-200 text-slate-500 font-bold text-xs py-2 rounded-lg hover:border-slate-300">Urgent</button>
              <button
                class="border border-slate-200 text-slate-500 font-bold text-xs py-2 rounded-lg hover:border-slate-300">Batch</button>
            </div>
          </div>

          <div class="grid grid-cols-2 gap-4">
            <div>
              <label class="block text-xs font-bold uppercase text-slate-500 mb-2">Origin Sys</label>
              <select
                class="w-full bg-slate-50 border border-slate-200 rounded-lg px-3 py-2.5 text-sm font-medium focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                <option>Warehouse (WMS)</option>
                <option>HRMS Core</option>
              </select>
            </div>
            <div>
              <label class="block text-xs font-bold uppercase text-slate-500 mb-2">Target Sys</label>
              <select
                class="w-full bg-slate-50 border border-slate-200 rounded-lg px-3 py-2.5 text-sm font-medium focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                <option>Finance API</option>
                <option>LMS Engine</option>
              </select>
            </div>
          </div>


          <div>
            <label class="block text-xs font-bold uppercase text-slate-500 mb-2">Content Type</label>
            <div class="flex border-b border-slate-200 mb-4">
              <button @click="attachmentType = 'text'"
                :class="[attachmentType === 'text' ? 'text-indigo-600 border-indigo-600' : 'text-slate-500 border-transparent hover:text-slate-700', 'pb-2 px-4 text-sm font-bold border-b-2 transition-colors']">
                Text Message
              </button>
              <button @click="attachmentType = 'pdf'"
                :class="[attachmentType === 'pdf' ? 'text-indigo-600 border-indigo-600' : 'text-slate-500 border-transparent hover:text-slate-700', 'pb-2 px-4 text-sm font-bold border-b-2 transition-colors']">
                PDF Document
              </button>
            </div>

            <div v-if="attachmentType === 'text'" class="animate-in fade-in slide-in-from-bottom-2 duration-300">
              <textarea rows="4"
                class="w-full bg-slate-50 border border-slate-200 rounded-lg px-4 py-3 text-sm text-slate-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 transition placeholder-slate-400"
                placeholder="Type your official correspondence here..."></textarea>
            </div>

            <div v-if="attachmentType === 'pdf'" class="animate-in fade-in slide-in-from-bottom-2 duration-300">
              <div
                class="border-2 border-dashed border-slate-300 rounded-xl p-8 flex flex-col items-center justify-center text-center hover:border-indigo-400 hover:bg-slate-50 transition-colors cursor-pointer group">
                <div
                  class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-full flex items-center justify-center mb-3 group-hover:scale-110 transition-transform">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
                  </svg>
                </div>
                <p class="text-sm font-bold text-slate-700">Click to upload PDF</p>
                <p class="text-xs text-slate-400 mt-1">or drag and drop file here</p>
              </div>
            </div>
          </div>

          <div class="pt-2">
            <button @click="showModal = false"
              class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-xl shadow-lg shadow-indigo-200 transition-all active:scale-[0.98]">
              Execute Transaction
            </button>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue';
import Sidebar from './components/layout/Sidebar.vue';
import TopHeader from './components/layout/TopHeader.vue';
import StatGrid from './components/dashboard/StatGrid.vue';
import ActivityFeed from './components/dashboard/ActivityFeed.vue';

const showModal = ref(false);
const attachmentType = ref('text');

const messages = ref([
  {
    id: 1,
    from: 'WMS',
    to: 'HRMS',
    category: 'Inventory',
    title: 'Low Stock Alert: IT Equipment',
    body: 'Monitor inventory below threshold (5 units). Requisition auto-drafted for review.',
    timestamp: 'Just now',
    financialImpact: false,
    amount: '0',
  },
  {
    id: 2,
    from: 'LMS',
    to: 'FIN',
    category: 'Payroll',
    title: 'Certification Bonus Triggered',
    body: 'Employee EMP_902 completed "Advanced Node.js". Auto-triggering one-time bonus.',
    timestamp: '12 mins ago',
    financialImpact: true,
    amount: '500.00',
  },
  {
    id: 3,
    from: 'AMS',
    to: 'HRMS',
    category: 'Attendance',
    title: 'Attendance Anomaly Detected',
    body: 'System flagged 3 consecutive late arrivals for Dept: Engineering.',
    timestamp: '45 mins ago',
    financialImpact: false,
    amount: '0',
  },
  {
    id: 4,
    from: 'HRMS',
    to: 'WMS',
    category: 'Onboarding',
    title: 'New Hire Equipment Request',
    body: 'Provisioning kit for Senior Dev (Laptop, Monitor, Peripherals).',
    timestamp: '1 hour ago',
    financialImpact: false,
    amount: '0',
  },
  {
    id: 5,
    from: 'FIN',
    to: 'HRMS',
    category: 'Payroll',
    title: 'Salary Disbursement Complete',
    body: 'Batch #9902 processed successfully. 142 employees paid.',
    timestamp: 'Yesterday',
    financialImpact: true,
    amount: '142k',
  }
]);
</script>
