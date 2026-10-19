<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محاكاة نظام SAP Fiori ERP</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Alpine.js -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    <!-- Google Font Cairo -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body {
            font-family: 'Cairo', sans-serif;
        }
        [x-cloak] { display: none !important; }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col" x-data="sapApp()">

    <!-- شريط التنقل العلوي (SAP Fiori Shell Bar) -->
    <header class="bg-[#0a6ed1] text-white shadow-md flex items-center justify-between px-6 py-3 z-30">
        <div class="flex items-center space-x-4 space-x-reverse">
            <!-- زر القائمة الجانبية -->
            <button @click="sidebarOpen = !sidebarOpen" class="p-1.5 hover:bg-blue-700 rounded-lg transition">
                <i data-lucide="menu" class="w-6 h-6"></i>
            </button>
            <!-- الشعار ونظام SAP -->
            <div class="flex items-center space-x-2 space-x-reverse">
                <div class="bg-white text-[#0a6ed1] font-black px-2.5 py-1 rounded text-sm tracking-wider">SAP</div>
                <span class="font-bold text-lg">نظام تخطيط موارد المؤسسات (ERP)</span>
            </div>
        </div>

        <!-- البحث السريع وأيقونات المستخدم -->
        <div class="flex items-center space-x-4 space-x-reverse">
            <div class="relative hidden md:block">
                <input type="text" placeholder="بحث في التطبيقات، الطلبات، المنتجات..." class="bg-blue-800 text-white placeholder-blue-300 text-sm rounded-lg px-4 py-1.5 pr-10 focus:outline-none focus:ring-2 focus:ring-white w-72">
                <i data-lucide="search" class="w-4 h-4 text-blue-300 absolute right-3 top-2.5"></i>
            </div>
            <button class="relative p-1.5 hover:bg-blue-700 rounded-lg transition">
                <i data-lucide="bell" class="w-5 h-5"></i>
                <span class="absolute top-1 left-1 bg-red-500 text-xs rounded-full w-4 h-4 flex items-center justify-center font-bold">3</span>
            </button>
            <div class="flex items-center space-x-2 space-x-reverse border-r border-blue-600 pr-4">
                <div class="w-9 h-9 rounded-full bg-blue-700 flex items-center justify-center font-bold text-sm">م م</div>
                <span class="text-sm font-semibold hidden sm:inline">محمد محمود (مدير النظام)</span>
            </div>
        </div>
    </header>

    <div class="flex flex-1 relative overflow-hidden">

        <!-- القائمة الجانبية (Sidebar) -->
        <aside :class="sidebarOpen ? 'translate-x-0' : 'translate-x-full md:translate-x-0 w-20'" class="bg-white border-l border-slate-200 transition-all duration-300 flex flex-col z-25 absolute md:relative h-full shadow-sm">
            <div class="py-4 flex flex-col space-y-1 px-2">
                <template x-for="item in navItems" :key="item.id">
                    <button @click="currentTab = item.id" 
                        :class="currentTab === item.id ? 'bg-blue-50 text-[#0a6ed1] font-bold' : 'text-slate-600 hover:bg-slate-50 hover:text-slate-900'"
                        class="flex items-center space-x-3 space-x-reverse px-3 py-3 rounded-xl transition text-sm">
                        <i :data-lucide="item.icon" class="w-5 h-5 shrink-0"></i>
                        <span x-show="sidebarOpen" x-transition class="truncate" x-text="item.label"></span>
                    </button>
                </template>
            </div>
        </aside>

        <!-- المحتوى الرئيسي -->
        <main class="flex-1 p-6 overflow-y-auto max-h-[calc(100vh-60px)]">

            <!-- 1. لوحة التحكم (Dashboard) -->
            <div x-show="currentTab === 'dashboard'" x-cloak class="space-y-6">
                <div class="flex justify-between items-center">
                    <div>
                        <h1 class="text-2xl font-black text-slate-900">لوحة التحكم الرئيسية (Fiori Overview)</h1>
                        <p
