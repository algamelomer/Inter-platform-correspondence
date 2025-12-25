<template>
    <header class="h-16 bg-white border-b border-slate-200 flex items-center justify-between px-6 sticky top-0 z-20">
        <!-- Left: Breadcrumbs -->
        <div class="flex items-center gap-4">
            <div class="flex items-center text-sm font-medium text-slate-500">
                <span class="hover:text-indigo-600 cursor-pointer transition-colors">Batu IPC</span>
                <span class="mx-2 text-slate-300">/</span>
                <span class="text-slate-900 font-bold">Dashboard Overview</span>
            </div>
        </div>

        <!-- Right: Actions -->
        <div class="flex items-center gap-4">
            <div class="relative hidden md:block">
                <Search class="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-slate-400" />
                <input type="text" placeholder="Search logs..."
                    class="pl-9 pr-4 py-1.5 bg-slate-50 border border-slate-200 rounded-full text-sm w-64 focus:outline-none focus:ring-2 focus:ring-indigo-500/20 focus:border-indigo-500 transition-all" />
            </div>

            <div class="w-px h-6 bg-slate-200 mx-1"></div>

            <button
                class="relative p-2 text-slate-400 hover:text-indigo-600 hover:bg-slate-50 rounded-full transition-colors">
                <Bell class="w-5 h-5" />
                <span class="absolute top-1.5 right-1.5 w-2 h-2 bg-rose-500 rounded-full border-2 border-white"></span>
            </button>

            <button class="p-2 text-slate-400 hover:text-indigo-600 hover:bg-slate-50 rounded-full transition-colors">
                <HelpCircle class="w-5 h-5" />
            </button>
        </div>
    </header>
</template>

<script setup>
import { Search, Bell, HelpCircle } from 'lucide-vue-next';
</script>
