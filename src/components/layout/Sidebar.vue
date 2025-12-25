<template>
    <aside
        class="w-64 bg-slate-900 text-slate-300 flex flex-col h-screen fixed left-0 top-0 z-30 transition-all duration-300">
        <!-- Logo -->
        <div class="h-16 flex items-center px-6 border-b border-slate-800 bg-slate-950">
            <div
                class="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center text-white font-bold mr-3 shadow-lg shadow-indigo-900/50">
                B</div>
            <h1 class="text-white font-bold tracking-tight text-lg">Batu<span class="text-indigo-500">IPC</span></h1>
        </div>

        <!-- Nav -->
        <nav class="flex-1 p-4 space-y-1 overflow-y-auto custom-scrollbar">
            <p class="px-3 text-xs font-bold uppercase tracking-wider text-slate-500 mb-2 mt-2">Core Platform</p>

            <a href="#"
                class="flex items-center gap-3 px-3 py-2.5 rounded-lg bg-indigo-600 text-white shadow-md shadow-indigo-900/20 group">
                <LayoutDashboard class="w-5 h-5" />
                <span class="font-medium text-sm">Dashboard</span>
            </a>

            <a href="#"
                class="flex items-center gap-3 px-3 py-2.5 rounded-lg hover:bg-slate-800 hover:text-white transition-colors group">
                <Server class="w-5 h-5 group-hover:text-indigo-400 transition-colors" />
                <span class="font-medium text-sm">Systems</span>
                <span
                    class="ml-auto text-[10px] font-bold bg-slate-800 text-emerald-500 px-1.5 py-0.5 rounded border border-slate-700">5</span>
            </a>

            <a href="#"
                class="flex items-center gap-3 px-3 py-2.5 rounded-lg hover:bg-slate-800 hover:text-white transition-colors group">
                <MessageSquareText class="w-5 h-5 group-hover:text-indigo-400 transition-colors" />
                <span class="font-medium text-sm">Correspondence</span>
            </a>

            <p class="px-3 text-xs font-bold uppercase tracking-wider text-slate-500 mb-2 mt-6">Analytics</p>

            <a href="#"
                class="flex items-center gap-3 px-3 py-2.5 rounded-lg hover:bg-slate-800 hover:text-white transition-colors group">
                <BarChart3 class="w-5 h-5 group-hover:text-indigo-400 transition-colors" />
                <span class="font-medium text-sm">Traffic Logs</span>
            </a>

            <a href="#"
                class="flex items-center gap-3 px-3 py-2.5 rounded-lg hover:bg-slate-800 hover:text-white transition-colors group">
                <Zap class="w-5 h-5 group-hover:text-indigo-400 transition-colors" />
                <span class="font-medium text-sm">Performance</span>
            </a>
        </nav>

        <!-- User Snippet -->
        <div class="p-4 border-t border-slate-800 bg-slate-900/50">
            <div class="flex items-center gap-3 px-2">
                <div
                    class="w-8 h-8 rounded-full bg-gradient-to-tr from-indigo-500 to-purple-500 border border-slate-700 shadow-sm">
                </div>
                <div class="flex-1 min-w-0">
                    <p class="text-sm font-medium text-white truncate">Admin User</p>
                    <p class="text-xs text-slate-500 truncate">admin@batu.dev</p>
                </div>
                <button class="text-slate-400 hover:text-white transition-colors">
                    <Settings class="w-4 h-4" />
                </button>
            </div>
        </div>
    </aside>
</template>

<script setup>
import {
    LayoutDashboard,
    Server,
    MessageSquareText,
    BarChart3,
    Zap,
    Settings
} from 'lucide-vue-next';
</script>

<style scoped>
.custom-scrollbar::-webkit-scrollbar {
    width: 4px;
}

.custom-scrollbar::-webkit-scrollbar-track {
    background: transparent;
}

.custom-scrollbar::-webkit-scrollbar-thumb {
    background: #334155;
    border-radius: 4px;
}
</style>
