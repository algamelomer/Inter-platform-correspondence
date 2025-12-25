<template>
    <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden flex flex-col h-[600px]">
        <!-- Header -->
        <div class="p-6 border-b border-slate-100 flex justify-between items-center bg-slate-50/50">
            <div>
                <h3 class="font-bold text-slate-800 text-lg">System Activity Log</h3>
                <p class="text-sm text-slate-500">Real-time inter-platform communication stream</p>
            </div>
            <div class="flex gap-2">
                <button
                    class="px-3 py-1.5 text-xs font-semibold text-slate-600 bg-white border border-slate-200 rounded-lg hover:bg-slate-50 transition shadow-sm">
                    Export Log
                </button>
                <button
                    class="px-3 py-1.5 text-xs font-semibold text-white bg-slate-800 border border-slate-800 rounded-lg hover:bg-slate-700 transition shadow-sm">
                    Live View
                </button>
            </div>
        </div>

        <!-- Feed Content -->
        <div class="flex-1 overflow-y-auto p-0 relative">
            <table class="w-full text-left border-collapse">
                <thead class="bg-slate-50 sticky top-0 z-10 shadow-sm">
                    <tr>
                        <th
                            class="px-6 py-3 text-xs font-bold text-slate-500 uppercase tracking-wider border-b border-slate-200">
                            Time</th>
                        <th
                            class="px-6 py-3 text-xs font-bold text-slate-500 uppercase tracking-wider border-b border-slate-200">
                            Type</th>
                        <th
                            class="px-6 py-3 text-xs font-bold text-slate-500 uppercase tracking-wider border-b border-slate-200">
                            Source / Target</th>
                        <th
                            class="px-6 py-3 text-xs font-bold text-slate-500 uppercase tracking-wider border-b border-slate-200">
                            Message</th>
                        <th
                            class="px-6 py-3 text-xs font-bold text-slate-500 uppercase tracking-wider border-b border-slate-200 text-right">
                            Action</th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-slate-100">
                    <tr v-for="msg in messages" :key="msg.id" class="hover:bg-slate-50/80 transition-colors group">
                        <td class="px-6 py-4 whitespace-nowrap text-xs font-mono text-slate-500">
                            {{ msg.timestamp }}
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span
                                :class="[getCategoryBadge(msg.category), 'text-[10px] font-bold px-2 py-1 rounded-md uppercase tracking-wide']">
                                {{ msg.category }}
                            </span>
                            <div v-if="msg.financialImpact"
                                class="mt-1 flex items-center gap-1 text-[10px] font-bold text-amber-600">
                                <span class="w-1.5 h-1.5 bg-amber-500 rounded-full"></span> ${{ msg.amount }}
                            </div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <div class="flex items-center gap-2">
                                <div
                                    class="flex items-center gap-1.5 px-2 py-1 bg-slate-100 rounded text-xs font-bold text-slate-600">
                                    {{ msg.from }}
                                </div>
                                <ArrowRight class="w-3 h-3 text-slate-400" />
                                <div
                                    class="flex items-center gap-1.5 px-2 py-1 bg-indigo-50 rounded text-xs font-bold text-indigo-600">
                                    {{ msg.to }}
                                </div>
                            </div>
                        </td>
                        <td class="px-6 py-4">
                            <p class="text-sm font-semibold text-slate-800">{{ msg.title }}</p>
                            <p
                                class="text-xs text-slate-500 line-clamp-1 mt-0.5 group-hover:line-clamp-none transition-all">
                                {{ msg.body }}</p>
                        </td>
                        <td class="px-6 py-4 text-right">
                            <button
                                class="text-slate-300 hover:text-indigo-600 p-1 rounded-full hover:bg-indigo-50 transition">
                                <MoreHorizontal class="w-4 h-4" />
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
import { ArrowRight, MoreHorizontal } from 'lucide-vue-next';

const props = defineProps({
    messages: Array
});

const getCategoryBadge = (cat) => {
    switch (cat.toLowerCase()) {
        case 'payroll': return 'bg-amber-100 text-amber-700';
        case 'attendance': return 'bg-emerald-100 text-emerald-700';
        case 'training': return 'bg-indigo-100 text-indigo-700';
        case 'inventory': return 'bg-rose-100 text-rose-700';
        default: return 'bg-slate-100 text-slate-700';
    }
};
</script>
