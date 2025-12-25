<template>
  <div class="min-h-screen bg-slate-50 font-sans antialiased text-slate-900">
    <nav class="bg-white border-b border-slate-200 px-6 py-4 flex justify-between items-center sticky top-0 z-10">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 bg-indigo-600 rounded-lg flex items-center justify-center text-white font-bold">H</div>
        <h1 class="text-xl font-bold tracking-tight">Inter-Platform Correspondence</h1>
      </div>
      <div class="flex gap-3">
        <button @click="showLogs = !showLogs" class="px-4 py-2 text-sm font-medium text-slate-600 hover:bg-slate-100 rounded-md transition">
          View Raw Logs
        </button>
        <button @click="openModal" class="px-4 py-2 text-sm font-medium bg-indigo-600 text-white hover:bg-indigo-700 rounded-md shadow-sm transition">
          New Dispatch
        </button>
      </div>
    </nav>

    <main class="max-w-7xl mx-auto p-6 space-y-8">
      
      <section class="grid grid-cols-1 md:grid-cols-4 gap-4">
        <div v-for="sys in systems" :key="sys.name" 
             class="bg-white p-5 rounded-xl border border-slate-200 shadow-xs flex items-center gap-4">
          <div :class="[sys.active ? 'bg-emerald-100 text-emerald-600' : 'bg-rose-100 text-rose-600', 'p-3 rounded-full']">
            <component :is="sys.icon" class="w-5 h-5" />
          </div>
          <div>
            <p class="text-xs font-semibold uppercase tracking-wider text-slate-500">{{ sys.name }}</p>
            <p class="text-sm font-bold">{{ sys.active ? 'Sync Active' : 'Offline' }}</p>
          </div>
        </div>
      </section>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        
        <section class="lg:col-span-2 space-y-4">
          <h2 class="text-lg font-bold flex items-center gap-2">
            Recent Interactions
            <span class="text-xs font-normal bg-slate-200 px-2 py-0.5 rounded-full text-slate-600">{{ filteredMessages.length }}</span>
          </h2>
          
          <div v-for="msg in filteredMessages" :key="msg.id" 
               class="bg-white p-5 rounded-xl border border-slate-200 hover:border-indigo-300 transition-colors shadow-sm group">
            <div class="flex justify-between items-start mb-3">
              <div class="flex items-center gap-2">
                <span :class="getCategoryClass(msg.category)" class="text-[10px] font-bold px-2 py-0.5 rounded uppercase">
                  {{ msg.category }}
                </span>
                <span class="text-slate-400 text-xs tracking-tighter">{{ msg.timestamp }}</span>
              </div>
              <span class="text-xs font-medium text-slate-500 group-hover:text-indigo-600 cursor-pointer italic">Details →</span>
            </div>
            
            <h3 class="font-semibold text-slate-800">{{ msg.title }}</h3>
            <p class="text-sm text-slate-600 mt-1 leading-relaxed">{{ msg.body }}</p>
            
            <div class="mt-4 pt-4 border-t border-slate-50 flex items-center justify-between">
              <div class="flex -space-x-2">
                <div class="w-6 h-6 rounded-full bg-slate-200 border-2 border-white text-[8px] flex items-center justify-center font-bold">
                  {{ msg.from }}
                </div>
                <div class="w-6 h-6 rounded-full bg-indigo-100 border-2 border-white text-[8px] flex items-center justify-center font-bold text-indigo-600">
                  {{ msg.to }}
                </div>
              </div>
              <span v-if="msg.financialImpact" class="text-xs font-bold text-amber-600 flex items-center gap-1">
                <span class="w-1.5 h-1.5 bg-amber-500 rounded-full animate-pulse"></span>
                Payroll Impact: ${{ msg.amount }}
              </span>
            </div>
          </div>
        </section>

        <aside class="space-y-6">
          <div class="bg-indigo-900 rounded-xl p-6 text-white shadow-xl shadow-indigo-200">
            <h3 class="font-bold mb-4">Inter-platform Logic</h3>
            <div class="space-y-4 text-sm opacity-90">
              <div class="flex justify-between border-b border-indigo-800 pb-2">
                <span>Avg. Sync Time</span>
                <span class="font-mono">1.2s</span>
              </div>
              <div class="flex justify-between border-b border-indigo-800 pb-2">
                <span>Pending Finance Approvals</span>
                <span class="font-mono">14</span>
              </div>
              <div class="flex justify-between">
                <span>Email Queue</span>
                <span class="font-mono">Healthy</span>
              </div>
            </div>
            <button class="w-full mt-6 py-2 bg-white/10 hover:bg-white/20 border border-white/20 rounded-lg text-xs font-bold transition">
              Run System Diagnostic
            </button>
          </div>
        </aside>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { 
  Users, 
  GraduationCap, 
  Clock, 
  CreditCard 
} from 'lucide-vue-next';

// Platform statuses
const systems = ref([
  { name: 'HRMS Core', icon: Users, active: true },
  { name: 'LMS Engine', icon: GraduationCap, active: true },
  { name: 'AMS Tracker', icon: Clock, active: true },
  { name: 'Finance API', icon: CreditCard, active: false }
]);

// Correspondence Mock Data
const messages = ref([
  {
    id: 1,
    from: 'LMS',
    to: 'PAY',
    category: 'Payroll',
    title: 'Certification Bonus Triggered',
    body: 'Employee EMP_902 completed "Advanced Node.js". Auto-triggering one-time bonus of $500.',
    timestamp: '2 mins ago',
    financialImpact: true,
    amount: '500.00'
  },
  {
    id: 2,
    from: 'AMS',
    to: 'HR',
    category: 'Attendance',
    title: 'Attendance Anomaly Detected',
    body: 'System flagged 3 consecutive late arrivals for Dept: Engineering. Notifications sent to manager.',
    timestamp: '45 mins ago',
    financialImpact: false
  },
  {
    id: 3,
    from: 'HR',
    to: 'LMS',
    category: 'Training',
    title: 'New Onboarding Sequence',
    body: 'User EMP_1024 added to HRMS. Syncing enrollment data for mandatory Safety Training.',
    timestamp: '2 hours ago',
    financialImpact: false
  }
]);

const filteredMessages = computed(() => messages.value);

const getCategoryClass = (cat) => {
  switch (cat.toLowerCase()) {
    case 'payroll': return 'bg-amber-100 text-amber-700';
    case 'attendance': return 'bg-emerald-100 text-emerald-700';
    case 'training': return 'bg-indigo-100 text-indigo-700';
    default: return 'bg-slate-100 text-slate-700';
  }
};

const openModal = () => alert("Open New Dispatch UI...");
</script>

<style>
/* Custom transitions for v4 */
.transition-all {
  transition-duration: 300ms;
}
</style>