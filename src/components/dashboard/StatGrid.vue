<template>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
        <div v-for="sys in systems" :key="sys.name"
            class="bg-white p-6 rounded-2xl border border-slate-100 shadow-sm hover:shadow-lg transition-all duration-300 group">
            <div class="flex justify-between items-start mb-4">
                <div
                    :class="[sys.active ? 'bg-emerald-50 text-emerald-600' : 'bg-rose-50 text-rose-600', 'p-3 rounded-xl transition-colors']">
                    <component :is="sys.icon" class="w-6 h-6" />
                </div>
                <span
                    :class="[sys.active ? 'text-emerald-600 bg-emerald-50 border-emerald-100' : 'text-rose-600 bg-rose-50 border-rose-100', 'text-[10px] font-bold px-2 py-1 rounded-full border uppercase tracking-wide']">
                    {{ sys.active ? 'Online' : 'Offline' }}
                </span>
            </div>

            <div>
                <h3 class="text-slate-500 font-medium text-xs uppercase tracking-wider mb-1">{{ sys.code }} Node</h3>
                <h2 class="text-xl font-bold text-slate-800 mb-2">{{ sys.name }}</h2>
                <div class="w-full bg-slate-100 h-1.5 rounded-full overflow-hidden">
                    <div :class="[sys.active ? 'bg-indigo-500' : 'bg-slate-300', 'h-full rounded-full transition-all duration-1000']"
                        :style="{ width: sys.load + '%' }"></div>
                </div>
                <div class="flex justify-between mt-2 text-xs text-slate-400 font-mono">
                    <span>Load</span>
                    <span>{{ sys.load }}%</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import {
    Users,
    GraduationCap,
    Clock,
    CreditCard,
    Package
} from 'lucide-vue-next';

const systems = ref([
    { name: 'HRMS Core', code: 'HRM-01', icon: Users, active: true, load: 45 },
    { name: 'LMS Engine', code: 'LMS-02', icon: GraduationCap, active: true, load: 72 },
    { name: 'AMS Tracker', code: 'AMS-V1', icon: Clock, active: true, load: 12 },
    { name: 'Finance API', code: 'FIN-X', icon: CreditCard, active: false, load: 0 },
    { name: 'Warehouse', code: 'WMS-PRO', icon: Package, active: true, load: 28 } // Added Warehouse
]);
</script>
