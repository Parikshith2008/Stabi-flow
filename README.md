<!DOCTYPE html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STABIFLOW — Your Income Changes. Your Stability Flows.</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Font: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        emerald: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            200: '#bbf7d0',
                            300: '#86efac',
                            400: '#4ade80',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            800: '#166534',
                            900: '#14532d',
                            950: '#052e16',
                        },
                        brand: {
                            bgEmerald: '#061a12',
                            cardEmerald: '#0b281c',
                            borderEmerald: '#133a2a',
                            bgNoir: '#090d0b',
                            cardNoir: '#121715',
                            borderNoir: '#1d2622',
                            bgLight: '#f5f7f6',
                            cardLight: '#ffffff',
                            borderLight: '#e2e8f0',
                            accent: '#22c55e',
                            accentHover: '#16a34a',
                            mint: '#34d399'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom Theme Styles */
        body {
            font-family: 'Inter', sans-serif;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        /* Scrollbar styling */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(34, 197, 94, 0.2);
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: rgba(34, 197, 94, 0.4);
        }

        /* Glassmorphism utilities */
        .glass-panel {
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }

        /* Themes setup */
        .theme-emerald {
            background-color: #061a12;
            color: #ecfdf5;
        }
        .theme-emerald .app-card {
            background-color: #0b281c;
            border-color: #154432;
        }
        .theme-emerald .app-sidebar {
            background-color: #04120c;
            border-color: #0d3122;
        }
        .theme-emerald .app-header {
            background-color: rgba(6, 26, 18, 0.8);
            border-color: #103828;
        }

        .theme-noir {
            background-color: #090d0b;
            color: #f0fdf4;
        }
        .theme-noir .app-card {
            background-color: #121715;
            border-color: #1d2622;
        }
        .theme-noir .app-sidebar {
            background-color: #050706;
            border-color: #141b18;
        }
        .theme-noir .app-header {
            background-color: rgba(9, 13, 11, 0.85);
            border-color: #1a231f;
        }

        .theme-light {
            background-color: #f4f7f5;
            color: #0f2419;
        }
        .theme-light .app-card {
            background-color: #ffffff;
            border-color: #e2e8f0;
            box-shadow: 0 4px 20px -2px rgba(0, 0, 0, 0.03);
        }
        .theme-light .app-sidebar {
            background-color: #ffffff;
            border-color: #e2e8f0;
        }
        .theme-light .app-header {
            background-color: rgba(244, 247, 245, 0.85);
            border-color: #e2e8f0;
        }
        .theme-light .text-muted {
            color: #64748b;
        }
        .theme-light .subtle-bg {
            background-color: #f8faf9;
        }
        .theme-emerald .text-muted, .theme-noir .text-muted {
            color: #9ca3af;
        }
        .theme-emerald .subtle-bg, .theme-noir .subtle-bg {
            background-color: rgba(255, 255, 255, 0.03);
        }

        /* Calendar highlight styling */
        .cal-day {
            min-height: 44px;
            cursor: pointer;
            transition: all 0.15s ease;
        }
        .cal-day:hover {
            transform: translateY(-1px);
        }
        .cal-day.selected {
            ring: 2px;
            outline: 2px solid #22c55e;
        }
    </style>
</head>
<body class="h-full theme-emerald antialiased selection:bg-emerald-500 selection:text-white" id="appBody">

    <!-- APP CONTAINER -->
    <div id="app" class="min-h-screen flex flex-col">
        <!-- RENDERED BY JS -->
    </div>

    <!-- MAIN JAVASCRIPT APP ENGINE -->
    <script>
        // ==========================================
        // DUMMY INITIAL DATA (MATCHING RECORDING)
        // ==========================================
        const INITIAL_DEMO_DATA = {
            user: {
                name: "Tousif",
                email: "tousif@example.com",
                occupation: "Tuition Teacher",
                incomeSource: "Fees",
                currency: "INR",
                incomeRange: "15,000 - 30,000",
                digestEnabled: true,
                alertsEnabled: true,
                onboarded: true
            },
            theme: "emerald", // 'emerald' | 'noir' | 'light'
            isAuthenticated: true,
            savings: {
                balance: 9600,
                target: 30000,
                history: [
                    { id: 's1', type: 'deposit', amount: 5000, date: '2026-09-15', note: 'Saved from monthly earnings' },
                    { id: 's2', type: 'deposit', amount: 5300, date: '2026-10-01', note: 'Monthly buffer reserve' },
                    { id: 's3', type: 'deposit', amount: 500, date: '2026-10-18', note: 'Added to savings' },
                    { id: 's4', type: 'deposit', amount: 3000, date: '2026-11-05', note: 'Set aside for low period' },
                    { id: 's5', type: 'withdraw', amount: 4200, date: '2026-11-18', note: 'Emergency vehicle repair' }
                ]
            },
            transactions: [
                { id: 't1', type: 'income', category: 'Delivery', amount: 2000, date: '2026-11-20', description: 'Evening delivery shifts' },
                { id: 't2', type: 'income', category: 'Delivery', amount: 4300, date: '2026-11-18', description: 'Weekend peak shift' },
                { id: 't3', type: 'expense', category: 'Fuel', amount: 200, date: '2026-11-18', description: 'Scooter refill' },
                { id: 't4', type: 'income', category: 'Cab driving', amount: 3100, date: '2026-11-16', description: 'Outstation trips' },
                { id: 't5', type: 'expense', category: 'Food', amount: 450, date: '2026-11-15', description: 'Lunch & tea' },
                { id: 't6', type: 'income', category: 'Freelancing', amount: 5200, date: '2026-10-22', description: 'Graphic design gig' },
                { id: 't7', type: 'expense', category: 'Vehicle maintenance', amount: 1500, date: '2026-10-18', description: 'Brake pad change' },
                { id: 't8', type: 'expense', category: 'Rent', amount: 3500, date: '2026-10-01', description: 'Room share rent' },
                { id: 't9', type: 'income', category: 'Salary', amount: 5200, date: '2026-10-05', description: 'Part time tuition' },
                { id: 't10', type: 'expense', category: 'Fuel', amount: 320, date: '2026-10-04', description: 'Weekly petrol' },
                { id: 't11', type: 'income', category: 'Delivery', amount: 1800, date: '2026-09-28', description: 'Evening batch' },
                { id: 't12', type: 'expense', category: 'Food', amount: 650, date: '2026-09-25', description: 'Groceries' },
                { id: 't13', type: 'income', category: 'Cab driving', amount: 2800, date: '2026-09-16', description: 'Airport trips' },
                { id: 't14', type: 'expense', category: 'Fuel', amount: 400, date: '2026-09-12', description: 'Fuel refill' }
            ]
        };

        // ==========================================
        // STATE STORE WITH LOCALSTORAGE PERSISTENCE
        // ==========================================
        class AppState {
            constructor() {
                this.load();
                this.activeTab = 'overview'; // 'overview' | 'transactions' | 'savings' | 'intelligence' | 'settings'
                const today = new Date();
                this.selectedCalendarDate = getLocalDateString(today);
                this.calendarViewMonth = today.getMonth();
                this.calendarViewYear = today.getFullYear();
                this.activeTxFilter = 'all'; // 'all' | 'income' | 'expense'
                this.txSearchQuery = '';
                this.txCategoryFilter = 'all';
                this.modalState = null; // null | 'addTx' | 'editTx' | 'savingsModal' | 'editTarget'
                this.editingTxId = null;
                this.notificationsOpen = false;
                this.notifications = [
                    { id: 1, title: "Income rhythm healthy", time: "10m ago", read: false },
                    { id: 2, title: "Savings target 32% reached", time: "2h ago", read: false },
                    { id: 3, title: "Welcome to STABIFLOW!", time: "1d ago", read: true }
                ];
            }

            load() {
                const saved = localStorage.getItem('STABIFLOW_DATA_V1');
                if (saved) {
                    try {
                        const parsed = JSON.parse(saved);
                        this.data = parsed;
                    } catch (e) {
                        this.data = JSON.parse(JSON.stringify(INITIAL_DEMO_DATA));
                    }
                } else {
                    this.data = JSON.parse(JSON.stringify(INITIAL_DEMO_DATA));
                }
            }

            save() {
                localStorage.setItem('STABIFLOW_DATA_V1', JSON.stringify(this.data));
                this.applyTheme();
                renderApp();
            }

            resetDemo() {
                this.data = JSON.parse(JSON.stringify(INITIAL_DEMO_DATA));
                this.save();
                showToast("Workspace reloaded with demo data");
            }

            clearData() {
                this.data.transactions = [];
                this.data.savings.balance = 0;
                this.data.savings.history = [];
                this.save();
                showToast("All financial records cleared");
            }

            applyTheme() {
                const body = document.getElementById('appBody');
                body.className = `h-full antialiased selection:bg-emerald-500 selection:text-white theme-${this.data.theme}`;
            }

            getCurrencySymbol() {
                const cur = this.data.user.currency || 'INR';
                switch(cur) {
                    case 'USD': return '$';
                    case 'EUR': return '€';
                    case 'GBP': return '£';
                    default: return '₹';
                }
            }

            // Calculation Rules Engine
            getCalculations() {
                const totalIncome = this.data.transactions
                    .filter(t => t.type === 'income')
                    .reduce((sum, t) => sum + Number(t.amount), 0);

                const totalExpenses = this.data.transactions
                    .filter(t => t.type === 'expense')
                    .reduce((sum, t) => sum + Number(t.amount), 0);

                const actualSavings = Number(this.data.savings.balance || 0);
                const availableBalance = totalIncome - totalExpenses - actualSavings;
                const monthlyRemaining = availableBalance;

                // Daily metrics
                const daysRecorded = new Set(this.data.transactions.map(t => t.date)).size || 1;
                const avgDailyIncome = Math.round(totalIncome / Math.max(daysRecorded, 1));
                const avgWeeklyIncome = Math.round(avgDailyIncome * 7);

                // Calculate stability score (0 to 100)
                let score = 50;
                if (totalIncome > 0) {
                    const savingsRatio = (actualSavings / totalIncome);
                    const expenseRatio = (totalExpenses / totalIncome);
                    score += Math.min(25, Math.round(savingsRatio * 50));
                    if (expenseRatio <= 0.7) score += 20;
                    if (this.data.transactions.length >= 5) score += 10;
                }
                score = Math.min(98, Math.max(20, score));

                return {
                    totalIncome,
                    totalExpenses,
                    availableBalance,
                    actualSavings,
                    monthlyRemaining,
                    avgDailyIncome,
                    avgWeeklyIncome,
                    stabilityScore: score
                };
            }
        }

        const state = new AppState();

        // Toast Notification System
        function showToast(message) {
            let toast = document.getElementById('stabiflow-toast');
            if (!toast) {
                toast = document.createElement('div');
                toast.id = 'stabiflow-toast';
                toast.className = 'fixed bottom-6 right-6 z-50 bg-emerald-600 text-white px-5 py-3 rounded-xl shadow-2xl flex items-center gap-3 transition-all transform translate-y-10 opacity-0 text-sm font-medium';
                document.body.appendChild(toast);
            }
            toast.innerHTML = `
                <svg class="w-5 h-5 text-emerald-100" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
                </svg>
                <span>${message}</span>
            `;
            setTimeout(() => {
                toast.classList.remove('translate-y-10', 'opacity-0');
            }, 10);
            setTimeout(() => {
                toast.classList.add('translate-y-10', 'opacity-0');
            }, 3000);
        }

        // CSV Exporter
        function exportCSV() {
            if (state.data.transactions.length === 0) {
                showToast("No transaction records to export");
                return;
            }
            const headers = ["ID", "Type", "Category", "Amount", "Date", "Description"];
            const rows = state.data.transactions.map(t => [
                t.id,
                t.type,
                `"${t.category}"`,
                t.amount,
                t.date,
                `"${(t.description || '').replace(/"/g, '""')}"`
            ]);
            const csvContent = "data:text/csv;charset=utf-8," + [headers.join(","), ...rows.map(e => e.join(","))].join("\n");
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `STABIFLOW_Transactions_${new Date().toISOString().slice(0,10)}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast("Transaction history exported to CSV");
        }

        // Formatting Helpers
        function getLocalDateString(date) {
            const year = date.getFullYear();
            const month = String(date.getMonth() + 1).padStart(2, '0');
            const day = String(date.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        }

        function formatMoney(amount) {
            const sym = state.getCurrencySymbol();
            return `${sym}${Number(amount).toLocaleString('en-IN')}`;
        }

        function getCategoryIcon(cat) {
            const icons = {
                'Cab driving': '<svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h8m-8 4h8m-4 4h4m-8 4h8M4 6h16M4 18h16"/></svg>',
                'Delivery': '<svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"/></svg>',
                'Freelancing': '<svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>',
                'Fuel': '<svg class="w-4 h-4 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>',
                'Food': '<svg class="w-4 h-4 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"/></svg>',
                'Vehicle maintenance': '<svg class="w-4 h-4 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/></svg>',
                'Rent': '<svg class="w-4 h-4 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"/></svg>'
            };
            return icons[cat] || '<svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>';
        }

        // ==========================================
        // RENDER: AUTHENTICATION & ONBOARDING
        // ==========================================
        function renderAuthScreen() {
            return `
            <div class="min-h-screen grid grid-cols-1 lg:grid-cols-12 bg-brand-bgEmerald">
                <!-- Left Brand Panel -->
                <div class="lg:col-span-6 xl:col-span-7 bg-gradient-to-br from-emerald-950 via-brand-bgEmerald to-black p-8 lg:p-16 flex flex-col justify-between relative overflow-hidden border-r border-emerald-900/30">
                    <div class="absolute -top-24 -left-24 w-96 h-96 bg-emerald-500/10 rounded-full blur-3xl"></div>
                    <div class="absolute bottom-0 right-0 w-80 h-80 bg-brand-accent/10 rounded-full blur-3xl"></div>

                    <!-- Header logo -->
                    <div class="relative z-10 flex items-center gap-3">
                        <div class="w-10 h-10 rounded-xl bg-emerald-500/20 border border-emerald-500/40 flex items-center justify-center text-emerald-400 shadow-lg">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/>
                            </svg>
                        </div>
                        <span class="text-2xl font-bold tracking-tight text-white">STABIFLOW</span>
                    </div>

                    <!-- Hero Messaging -->
                    <div class="relative z-10 my-16 max-w-xl">
                        <div class="text-emerald-400 text-5xl font-extrabold mb-4 opacity-30">“</div>
                        <h1 class="text-4xl sm:text-5xl font-extrabold text-white leading-tight mb-6 tracking-tight">
                            Your income changes.<br/>
                            <span class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 to-mint">Your stability flows.</span>
                        </h1>
                        <p class="text-lg text-emerald-200/80 leading-relaxed">
                            Built for the people who keep the world moving, one day at a time. Empowering drivers, freelancers, delivery partners, and self-employed leaders to smooth out irregular income.
                        </p>

                        <!-- Stats Badge Row -->
                        <div class="mt-12 grid grid-cols-2 gap-4 pt-8 border-t border-emerald-800/40">
                            <div>
                                <div class="text-2xl font-bold text-white">₹18.4k</div>
                                <div class="text-xs text-emerald-300/60 uppercase tracking-wider font-semibold">Average monthly shift</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-white">4.8 / 5</div>
                                <div class="text-xs text-emerald-300/60 uppercase tracking-wider font-semibold">Independent earners</div>
                            </div>
                        </div>
                    </div>

                    <div class="relative z-10 text-xs text-emerald-500/60">
                        &copy; 2026 STABIFLOW Platform. Designed for modern irregular incomes.
                    </div>
                </div>

                <!-- Right Login Form -->
                <div class="lg:col-span-6 xl:col-span-5 flex items-center justify-center p-6 sm:p-12 bg-brand-bgNoir">
                    <div class="w-full max-w-md app-card p-8 rounded-3xl border border-emerald-900/40 shadow-2xl bg-brand-cardNoir">
                        <div class="mb-8">
                            <span class="text-xs font-bold tracking-widest text-emerald-400 uppercase">Welcome Back</span>
                            <h2 class="text-2xl font-bold text-white mt-1">Good to see you again.</h2>
                            <p class="text-sm text-gray-400 mt-1">Your money story is one claim pass.</p>
                        </div>

                        <form onsubmit="handleAuthSubmit(event)" class="space-y-5">
                            <div>
                                <label class="block text-xs font-medium text-gray-300 uppercase mb-2">Email address</label>
                                <input type="email" id="authEmail" required value="tousif@example.com" class="w-full bg-brand-bgNoir border border-emerald-900/60 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-emerald-500 transition-colors text-sm" placeholder="you@example.com">
                            </div>

                            <div>
                                <label class="block text-xs font-medium text-gray-300 uppercase mb-2">Password</label>
                                <div class="relative">
                                    <input type="password" id="authPassword" required value="password123" class="w-full bg-brand-bgNoir border border-emerald-900/60 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-emerald-500 transition-colors text-sm" placeholder="••••••••">
                                    <button type="button" onclick="togglePasswordVisibility()" class="absolute right-3 top-3 text-gray-400 hover:text-white text-xs">
                                        Show
                                    </button>
                                </div>
                            </div>

                            <div class="flex items-center justify-between text-xs">
                                <label class="flex items-center gap-2 text-gray-400 cursor-pointer">
                                    <input type="checkbox" checked class="rounded border-emerald-900 text-emerald-500 focus:ring-0 bg-transparent">
                                    <span>Remember me</span>
                                </label>
                                <a href="#" onclick="showToast('Demo mode active - click Sign In'); return false;" class="text-emerald-400 hover:underline">Forgot password?</a>
                            </div>

                            <button type="submit" class="w-full bg-emerald-500 hover:bg-emerald-600 text-black font-semibold py-3.5 px-4 rounded-xl shadow-lg transition-all flex items-center justify-center gap-2 text-sm">
                                <span>Sign In</span>
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"/>
                                </svg>
                            </button>
                        </form>

                        <div class="mt-8 pt-6 border-t border-emerald-900/30 text-center space-y-4">
                            <button onclick="handleQuickDemoAccess()" class="w-full bg-emerald-950/80 hover:bg-emerald-900/80 text-emerald-300 border border-emerald-700/50 py-3 rounded-xl text-xs font-semibold transition-all">
                                Load Demo Workspace (Tousif)
                            </button>

                            <p class="text-xs text-gray-500">
                                Demo access is ready — any email & password work instantly.
                            </p>
                        </div>
                    </div>
                </div>
            </div>
            `;
        }

        function togglePasswordVisibility() {
            const pwd = document.getElementById('authPassword');
            if (pwd.type === 'password') {
                pwd.type = 'text';
            } else {
                pwd.type = 'password';
            }
        }

        function handleAuthSubmit(e) {
            e.preventDefault();
            const email = document.getElementById('authEmail').value;
            state.data.user.email = email;
            state.data.isAuthenticated = true;
            state.save();
        }

        function handleQuickDemoAccess() {
            state.data = JSON.parse(JSON.stringify(INITIAL_DEMO_DATA));
            state.data.isAuthenticated = true;
            state.save();
            showToast("Logged in to demo workspace");
        }

        // ==========================================
        // RENDER: APP NAVIGATION SIDEBAR & HEADER
        // ==========================================
        function renderSidebar() {
            const calcs = state.getCalculations();
            const user = state.data.user;

            const navItems = [
                { id: 'overview', label: 'Financial Overview', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"/></svg>' },
                { id: 'transactions', label: 'Transactions', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"/></svg>' },
                { id: 'savings', label: 'Savings', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z"/></svg>' },
                { id: 'intelligence', label: 'Financial Intelligence', badge: 'NEW', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>' },
                { id: 'settings', label: 'Settings', icon: '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/></svg>' }
            ];

            return `
            <aside class="w-64 app-sidebar flex flex-col justify-between p-4 border-r fixed inset-y-0 left-0 z-30 transition-transform duration-300 transform -translate-x-full md:translate-x-0" id="mainSidebar">
                <div>
                    <!-- Logo Header -->
                    <div class="px-3 py-4 flex items-center justify-between">
                        <div class="flex items-center gap-3 cursor-pointer" onclick="setActiveTab('overview')">
                            <div class="w-9 h-9 rounded-xl bg-emerald-500/20 border border-emerald-500/40 flex items-center justify-center text-emerald-400">
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/>
                                </svg>
                            </div>
                            <div>
                                <span class="font-bold text-lg text-current tracking-tight">STABIFLOW</span>
                                <div class="text-[10px] text-muted tracking-widest uppercase font-semibold -mt-1">income · stability</div>
                            </div>
                        </div>
                        <button onclick="toggleMobileSidebar()" class="md:hidden text-muted hover:text-current">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
                        </button>
                    </div>

                    <!-- Navigation Links -->
                    <div class="mt-6 space-y-1">
                        <div class="px-3 text-[10px] uppercase font-bold tracking-wider text-muted mb-2">Workspace</div>
                        ${navItems.map(item => {
                            const isActive = state.activeTab === item.id;
                            return `
                            <button onclick="setActiveTab('${item.id}')" class="w-full flex items-center justify-between px-3 py-2.5 rounded-xl text-sm font-medium transition-all ${isActive ? 'bg-emerald-500/15 text-emerald-400 font-semibold border border-emerald-500/20' : 'text-muted hover:text-current hover:bg-emerald-500/5'}">
                                <div class="flex items-center gap-3">
                                    ${item.icon}
                                    <span>${item.label}</span>
                                </div>
                                ${item.badge ? `<span class="bg-emerald-500/20 text-emerald-400 text-[10px] font-bold px-1.5 py-0.5 rounded-full border border-emerald-500/30">${item.badge}</span>` : ''}
                            </button>
                            `;
                        }).join('')}
                    </div>
                </div>

                <!-- Bottom Widgets & User Profile -->
                <div class="space-y-4 pt-4 border-t border-emerald-900/20">
                    <!-- Stability Score Card -->
                    <div class="p-3.5 rounded-2xl subtle-bg border border-emerald-900/30 space-y-2">
                        <div class="flex items-center justify-between text-xs">
                            <span class="font-semibold text-muted">Stability score</span>
                            <span class="text-emerald-400 font-bold">${calcs.stabilityScore} <span class="text-[10px] text-muted font-normal">/ 100</span></span>
                        </div>
                        <div class="w-full bg-emerald-950/50 rounded-full h-2 overflow-hidden border border-emerald-900/40">
                            <div class="bg-gradient-to-r from-emerald-500 to-mint h-full rounded-full" style="width: ${calcs.stabilityScore}%"></div>
                        </div>
                        <div class="text-[10px] text-muted flex items-center gap-1">
                            <span class="text-emerald-400 font-semibold">+4 points</span> this month
                        </div>
                    </div>

                    <!-- User Profile Footer -->
                    <div class="flex items-center justify-between px-1">
                        <div class="flex items-center gap-3">
                            <div class="w-9 h-9 rounded-full bg-emerald-500/20 text-emerald-400 font-bold flex items-center justify-center text-sm border border-emerald-500/40">
                                ${user.name.charAt(0).toUpperCase()}
                            </div>
                            <div class="overflow-hidden">
                                <div class="text-xs font-bold text-current truncate">${user.name}</div>
                                <div class="text-[10px] text-muted truncate">${user.occupation}</div>
                            </div>
                        </div>
                        <button onclick="handleLogout()" title="Sign Out" class="text-muted hover:text-red-400 p-1.5 rounded-lg transition-colors">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"/></svg>
                        </button>
                    </div>
                </div>
            </aside>
            `;
        }

        function renderHeader() {
            const todayStr = new Intl.DateTimeFormat('en-IN', { weekday: 'long', day: 'numeric', month: 'long', year: 'numeric' }).format(new Date());
            const unreadCount = state.notifications.filter(n => !n.read).length;

            return `
            <header class="app-header sticky top-0 z-20 backdrop-blur-md border-b px-4 lg:px-8 py-3.5 flex items-center justify-between">
                <div class="flex items-center gap-3">
                    <button onclick="toggleMobileSidebar()" class="md:hidden text-muted hover:text-current p-1.5 rounded-lg border border-emerald-900/30">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/></svg>
                    </button>
                    <div class="flex items-center gap-2 text-xs">
                        <span class="text-muted">Workspace</span>
                        <span class="text-muted">/</span>
                        <span class="font-semibold text-emerald-400 capitalize">${state.activeTab.replace('-', ' ')}</span>
                    </div>
                </div>

                <div class="flex items-center gap-4">
                    <!-- Date pill -->
                    <div class="hidden sm:flex items-center gap-2 text-xs text-muted font-medium bg-emerald-500/5 px-3 py-1.5 rounded-xl border border-emerald-500/10">
                        <svg class="w-3.5 h-3.5 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/></svg>
                        <span>${todayStr}</span>
                    </div>

                    <!-- Theme Switcher Pill -->
                    <div class="flex items-center subtle-bg rounded-xl p-1 border border-emerald-900/30">
                        <button onclick="setTheme('emerald')" title="Emerald Theme" class="px-2 py-1 rounded-lg text-xs font-medium transition-colors ${state.data.theme === 'emerald' ? 'bg-emerald-500 text-black font-semibold' : 'text-muted hover:text-current'}">Emerald</button>
                        <button onclick="setTheme('noir')" title="Noir Theme" class="px-2 py-1 rounded-lg text-xs font-medium transition-colors ${state.data.theme === 'noir' ? 'bg-emerald-500 text-black font-semibold' : 'text-muted hover:text-current'}">Noir</button>
                        <button onclick="setTheme('light')" title="Light Theme" class="px-2 py-1 rounded-lg text-xs font-medium transition-colors ${state.data.theme === 'light' ? 'bg-emerald-600 text-white font-semibold' : 'text-muted hover:text-current'}">Light</button>
                    </div>

                    <!-- Notifications Dropdown Trigger -->
                    <div class="relative">
                        <button onclick="toggleNotifications()" class="relative p-2 rounded-xl text-muted hover:text-current hover:bg-emerald-500/10 transition-colors">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 01-6 0v-1m6 0H9"/></svg>
                            ${unreadCount > 0 ? `<span class="absolute top-1.5 right-1.5 w-2 h-2 rounded-full bg-emerald-400"></span>` : ''}
                        </button>

                        <!-- Notifications Dropdown Box -->
                        ${state.notificationsOpen ? `
                        <div class="absolute right-0 mt-2 w-80 app-card rounded-2xl shadow-2xl border border-emerald-900/40 p-4 z-50">
                            <div class="flex items-center justify-between mb-3 pb-2 border-b border-emerald-900/20">
                                <span class="text-xs font-bold uppercase text-muted tracking-wider">Notifications</span>
                                <button onclick="markAllNotificationsRead()" class="text-[10px] text-emerald-400 hover:underline">Mark read</button>
                            </div>
                            <div class="space-y-2 max-h-60 overflow-y-auto">
                                ${state.notifications.map(n => `
                                    <div class="p-2.5 rounded-xl subtle-bg border border-emerald-900/20 flex items-start gap-2 text-xs">
                                        <div class="w-2 h-2 rounded-full bg-emerald-400 mt-1.5"></div>
                                        <div>
                                            <div class="font-medium text-current">${n.title}</div>
                                            <div class="text-[10px] text-muted mt-0.5">${n.time}</div>
                                        </div>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                        ` : ''}
                    </div>
                </div>
            </header>
            `;
        }

        // ==========================================
        // PAGE 1: FINANCIAL OVERVIEW
        // ==========================================
        function renderOverviewPage() {
            const calcs = state.getCalculations();
            const user = state.data.user;

            // Compute category totals for Donut
            const expCategories = {};
            state.data.transactions.filter(t => t.type === 'expense').forEach(t => {
                expCategories[t.category] = (expCategories[t.category] || 0) + Number(t.amount);
            });

            return `
            <div class="space-y-6 pb-12">
                <!-- Header Greeting -->
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <div class="text-xs font-semibold text-emerald-400 uppercase tracking-widest">${new Intl.DateTimeFormat('en-IN', { weekday: 'long', day: 'numeric', month: 'long' }).format(new Date())}</div>
                        <h1 class="text-2xl sm:text-3xl font-extrabold text-current tracking-tight mt-0.5">Good morning, ${user.name}.</h1>
                        <p class="text-xs sm:text-sm text-muted mt-1">Here's your financial pulse for the month so far.</p>
                    </div>
                    <div>
                        <button onclick="openAddTxModal()" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-4 py-2.5 rounded-xl shadow-lg transition-all flex items-center gap-2 text-sm">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
                            <span>Add transaction</span>
                        </button>
                    </div>
                </div>

                <!-- 4 KPI Cards -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <!-- Total Income -->
                    <div class="app-card p-5 rounded-2xl border transition-all hover:border-emerald-500/40">
                        <div class="flex items-center justify-between text-xs text-muted mb-2">
                            <span>Total income</span>
                            <span class="text-emerald-400 font-bold bg-emerald-500/10 px-2 py-0.5 rounded-full">+12.4% vs last month</span>
                        </div>
                        <div class="text-2xl font-bold text-current">${formatMoney(calcs.totalIncome)}</div>
                        <div class="text-[11px] text-muted mt-2 flex items-center gap-1">
                            <span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>
                            <span>From recorded shift entries</span>
                        </div>
                    </div>

                    <!-- Total Expenses -->
                    <div class="app-card p-5 rounded-2xl border transition-all hover:border-emerald-500/40">
                        <div class="flex items-center justify-between text-xs text-muted mb-2">
                            <span>Total expenses</span>
                            <span class="text-amber-400 font-bold bg-amber-500/10 px-2 py-0.5 rounded-full">-5.2% vs last month</span>
                        </div>
                        <div class="text-2xl font-bold text-current">${formatMoney(calcs.totalExpenses)}</div>
                        <div class="text-[11px] text-muted mt-2 flex items-center gap-1">
                            <span class="w-1.5 h-1.5 rounded-full bg-amber-400"></span>
                            <span>Across essential & personal spending</span>
                        </div>
                    </div>

                    <!-- Available Balance -->
                    <div class="app-card p-5 rounded-2xl border transition-all hover:border-emerald-500/40">
                        <div class="flex items-center justify-between text-xs text-muted mb-2">
                            <span>Available balance</span>
                            <span class="text-emerald-400 font-bold bg-emerald-500/10 px-2 py-0.5 rounded-full">+18.2% vs last month</span>
                        </div>
                        <div class="text-2xl font-bold text-emerald-400">${formatMoney(calcs.availableBalance)}</div>
                        <div class="text-[11px] text-muted mt-2">
                            <span>Income minus expenses (Never double-subtracted)</span>
                        </div>
                    </div>

                    <!-- Actual Savings -->
                    <div class="app-card p-5 rounded-2xl border transition-all hover:border-emerald-500/40">
                        <div class="flex items-center justify-between text-xs text-muted mb-2">
                            <span>Actual savings</span>
                            <span class="text-emerald-400 font-bold bg-emerald-500/10 px-2 py-0.5 rounded-full">+7.1% this month</span>
                        </div>
                        <div class="text-2xl font-bold text-current">${formatMoney(calcs.actualSavings)}</div>
                        <div class="text-[11px] text-muted mt-2">
                            <span>Manually saved separate balance</span>
                        </div>
                    </div>
                </div>

                <!-- Charts Section: Income vs Expenses & Breakdown -->
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Cashflow Chart -->
                    <div class="lg:col-span-8 app-card p-6 rounded-2xl border">
                        <div class="flex items-center justify-between mb-4">
                            <div>
                                <h3 class="text-base font-bold text-current">Income vs expenses</h3>
                                <p class="text-xs text-muted">Monthly cash flow trend</p>
                            </div>
                            <div class="flex items-center gap-4 text-xs font-medium">
                                <span class="flex items-center gap-1.5"><span class="w-2.5 h-2.5 rounded-full bg-emerald-500"></span> Income</span>
                                <span class="flex items-center gap-1.5"><span class="w-2.5 h-2.5 rounded-full bg-amber-500"></span> Expenses</span>
                            </div>
                        </div>
                        <div class="h-64 relative">
                            <canvas id="overviewFlowChart"></canvas>
                        </div>
                    </div>

                    <!-- Expense Breakdown Donut -->
                    <div class="lg:col-span-4 app-card p-6 rounded-2xl border flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="text-base font-bold text-current">Expense breakdown</h3>
                                <button onclick="setActiveTab('transactions')" class="text-xs text-emerald-400 hover:underline">View all</button>
                            </div>
                            <p class="text-xs text-muted mb-4">Where your money went</p>
                            <div class="h-44 relative flex items-center justify-center">
                                <canvas id="expenseDonutChart"></canvas>
                            </div>
                        </div>

                        <!-- Legend List -->
                        <div class="space-y-2 mt-4 pt-4 border-t border-emerald-900/20 text-xs">
                            ${Object.entries(expCategories).slice(0, 4).map(([cat, amt]) => `
                                <div class="flex items-center justify-between">
                                    <div class="flex items-center gap-2 text-muted">
                                        <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
                                        <span>${cat}</span>
                                    </div>
                                    <span class="font-semibold text-current">${formatMoney(amt)}</span>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </div>

                <!-- Financial Insight & Next Best Move -->
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Financial Insight Card -->
                    <div class="lg:col-span-7 app-card p-6 rounded-2xl border flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-2">
                                <div class="flex items-center gap-2">
                                    <svg class="w-5 h-5 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>
                                    <h3 class="text-base font-bold text-current">Your financial insight</h3>
                                </div>
                                <span class="text-[10px] uppercase font-bold text-emerald-400 bg-emerald-500/10 px-2.5 py-1 rounded-full border border-emerald-500/20">LIVE</span>
                            </div>
                            <p class="text-xs text-muted mb-4">Based on your records this month</p>
                            
                            <p class="text-sm text-current leading-relaxed">
                                You're keeping <span class="font-bold text-emerald-400">${calcs.totalIncome > 0 ? Math.round((calcs.availableBalance / calcs.totalIncome)*100) : 0}%</span> after expenses. Your income is trending upward — setting aside even ${formatMoney(1000)} could create a meaningful safety buffer.
                            </p>
                        </div>

                        <div class="mt-6 pt-4 border-t border-emerald-900/20">
                            <button onclick="setActiveTab('intelligence')" class="text-xs font-semibold text-emerald-400 hover:text-emerald-300 flex items-center gap-1">
                                <span>Explore Intelligence</span>
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"/></svg>
                            </button>
                        </div>
                    </div>

                    <!-- Next Best Move (How Much Can You Save?) -->
                    <div class="lg:col-span-5 app-card p-6 rounded-2xl border flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="text-xs uppercase tracking-widest font-bold text-muted">NEXT BEST MOVE</h3>
                                <button onclick="openSavingsModal()" class="bg-emerald-500 hover:bg-emerald-600 text-black text-xs font-semibold px-3 py-1.5 rounded-lg transition-all flex items-center gap-1">
                                    <span>Add to savings</span>
                                    <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
                                </button>
                            </div>
                            <h4 class="text-lg font-bold text-current mt-1">How much can you save?</h4>
                            <p class="text-xs text-muted mt-2 leading-relaxed">
                                You have <span class="text-emerald-400 font-bold">${formatMoney(calcs.availableBalance)}</span> left after recorded expenses. We suggest considering putting <span class="text-emerald-400 font-bold">${formatMoney(Math.round(calcs.availableBalance * 0.4))}</span> into your safety net.
                            </p>
                        </div>

                        <div class="mt-6 text-[11px] text-muted flex items-center gap-2">
                            <svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                            <span>Moving money to savings does not count as an expense.</span>
                        </div>
                    </div>
                </div>

                <!-- Recent Transactions Row -->
                <div class="app-card p-6 rounded-2xl border">
                    <div class="flex items-center justify-between mb-4">
                        <div>
                            <h3 class="text-base font-bold text-current">Recent transactions</h3>
                            <p class="text-xs text-muted">Your latest money moves</p>
                        </div>
                        <button onclick="setActiveTab('transactions')" class="text-xs font-semibold text-emerald-400 hover:underline">View all &rarr;</button>
                    </div>

                    <div class="space-y-3">
                        ${state.data.transactions.slice(0, 4).map(t => `
                            <div class="flex items-center justify-between p-3 rounded-xl subtle-bg border border-emerald-900/10">
                                <div class="flex items-center gap-3">
                                    <div class="w-9 h-9 rounded-xl bg-emerald-500/10 flex items-center justify-center border border-emerald-500/20">
                                        ${getCategoryIcon(t.category)}
                                    </div>
                                    <div>
                                        <div class="text-xs font-bold text-current">${t.category}</div>
                                        <div class="text-[10px] text-muted">${t.description || 'No description'}</div>
                                    </div>
                                </div>
                                <div class="text-right">
                                    <div class="text-xs font-bold ${t.type === 'income' ? 'text-emerald-400' : 'text-amber-400'}">
                                        ${t.type === 'income' ? '+' : '-'}${formatMoney(t.amount)}
                                    </div>
                                    <div class="text-[10px] text-muted">${t.date}</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>

                <!-- DAILY REPORTS: Monthly Calendar Grid & Side Panel -->
                <div class="app-card p-6 rounded-2xl border">
                    <div class="flex items-center justify-between mb-6">
                        <div>
                            <span class="text-xs uppercase font-bold tracking-widest text-muted">DAILY REPORTS</span>
                            <h3 class="text-lg font-bold text-current">Activity by day</h3>
                        </div>
                        <div class="flex items-center gap-2 text-xs">
                            <select aria-label="Calendar month" onchange="setCalendarMonth(this.value)" class="subtle-bg border border-emerald-900/30 rounded-lg px-2 py-1 text-current">
                                ${Array.from({length: 12}, (_, month) => `<option value="${month}" ${state.calendarViewMonth === month ? 'selected' : ''}>${new Date(2000, month, 1).toLocaleString('en-IN', { month: 'long' })}</option>`).join('')}
                            </select>
                            <select aria-label="Calendar year" onchange="setCalendarYear(this.value)" class="subtle-bg border border-emerald-900/30 rounded-lg px-2 py-1 text-current">
                                ${Array.from({length: 11}, (_, index) => state.calendarViewYear - 5 + index).map(year => `<option value="${year}" ${state.calendarViewYear === year ? 'selected' : ''}>${year}</option>`).join('')}
                            </select>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
                        <!-- Calendar Grid (7 columns) -->
                        <div class="lg:col-span-7">
                            <div class="grid grid-cols-7 gap-2 text-center text-xs font-bold text-muted mb-3">
                                <div>M</div><div>T</div><div>W</div><div>T</div><div>F</div><div>S</div><div>S</div>
                            </div>
                            <div class="grid grid-cols-7 gap-2" id="calendarGrid">
                                <!-- Populated dynamically by JS -->
                            </div>
                        </div>

                        <!-- Daily Detail Panel -->
                        <div class="lg:col-span-5 subtle-bg p-5 rounded-2xl border border-emerald-900/20 flex flex-col justify-between" id="dailyDetailPanel">
                            <!-- Populated dynamically based on selected day -->
                        </div>
                    </div>
                </div>
            </div>
            `;
        }

        // Render Calendar Days
        function renderCalendar() {
            const grid = document.getElementById('calendarGrid');
            if (!grid) return;

            const year = state.calendarViewYear;
            const month = state.calendarViewMonth;
            const firstWeekday = (new Date(year, month, 1).getDay() + 6) % 7;
            const daysInMonth = new Date(year, month + 1, 0).getDate();
            const todayStr = getLocalDateString(new Date());
            let html = '';

            // Empty cells align the first day with the Monday-first weekday headings.
            for (let blank = 0; blank < firstWeekday; blank++) {
                html += '<div class="cal-day p-2"></div>';
            }

            for (let day = 1; day <= daysInMonth; day++) {
                const dayStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                const txsOnDay = state.data.transactions.filter(t => t.date === dayStr);
                const hasIncome = txsOnDay.some(t => t.type === 'income');
                const hasExpense = txsOnDay.some(t => t.type === 'expense');
                const isSelected = state.selectedCalendarDate === dayStr;
                const isToday = todayStr === dayStr;

                html += `
                <div onclick="selectCalendarDate('${dayStr}')" class="cal-day p-2 rounded-xl border text-center relative flex flex-col items-center justify-center ${isSelected ? 'selected bg-emerald-500/20 border-emerald-500 font-bold' : 'subtle-bg border-emerald-900/20'} ${isToday ? 'ring-1 ring-emerald-400' : ''}">
                    <span class="text-xs text-current">${day}</span>
                    <div class="flex items-center gap-1 mt-1">
                        ${hasIncome ? `<span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>` : ''}
                        ${hasExpense ? `<span class="w-1.5 h-1.5 rounded-full bg-amber-400"></span>` : ''}
                    </div>
                </div>
                `;
            }
            grid.innerHTML = html;
            renderDailyDetailPanel();
        }

        function setCalendarMonth(month) {
            state.calendarViewMonth = Number(month);
            renderCalendar();
        }

        function setCalendarYear(year) {
            state.calendarViewYear = Number(year);
            renderCalendar();
        }

        function selectCalendarDate(dateStr) {
            state.selectedCalendarDate = dateStr;
            const selected = new Date(`${dateStr}T12:00:00`);
            state.calendarViewMonth = selected.getMonth();
            state.calendarViewYear = selected.getFullYear();
            renderCalendar();
        }

        function renderDailyDetailPanel() {
            const panel = document.getElementById('dailyDetailPanel');
            if (!panel) return;

            const dateStr = state.selectedCalendarDate;
            const txs = state.data.transactions.filter(t => t.date === dateStr);

            const dayEarned = txs.filter(t => t.type === 'income').reduce((s, t) => s + Number(t.amount), 0);
            const daySpent = txs.filter(t => t.type === 'expense').reduce((s, t) => s + Number(t.amount), 0);
            const dayRemaining = dayEarned - daySpent;

            panel.innerHTML = `
                <div>
                    <div class="text-xs uppercase font-bold text-emerald-400 tracking-wider mb-1">${dateStr}</div>
                    <div class="text-sm font-semibold text-current mb-4">Daily summary report</div>

                    <div class="grid grid-cols-3 gap-2 mb-4 text-center">
                        <div class="p-2 rounded-xl bg-emerald-500/10 border border-emerald-500/20">
                            <div class="text-[10px] text-muted font-medium uppercase">Earned</div>
                            <div class="text-xs font-bold text-emerald-400">${formatMoney(dayEarned)}</div>
                        </div>
                        <div class="p-2 rounded-xl bg-amber-500/10 border border-amber-500/20">
                            <div class="text-[10px] text-muted font-medium uppercase">Spent</div>
                            <div class="text-xs font-bold text-amber-400">${formatMoney(daySpent)}</div>
                        </div>
                        <div class="p-2 rounded-xl bg-blue-500/10 border border-blue-500/20">
                            <div class="text-[10px] text-muted font-medium uppercase">Remaining</div>
                            <div class="text-xs font-bold text-current">${formatMoney(dayRemaining)}</div>
                        </div>
                    </div>

                    <div class="space-y-2 max-h-48 overflow-y-auto">
                        ${txs.length === 0 ? `
                            <div class="text-center py-6 text-xs text-muted space-y-2">
                                <p>No transactions recorded for this day.</p>
                                <button onclick="openAddTxModal('${dateStr}')" class="text-emerald-400 font-semibold hover:underline">+ Add entry for this date</button>
                            </div>
                        ` : txs.map(t => `
                            <div class="p-2.5 rounded-xl app-card border border-emerald-900/20 flex items-center justify-between text-xs">
                                <div>
                                    <div class="font-bold text-current">${t.category}</div>
                                    <div class="text-[10px] text-muted">${t.description || 'No note'}</div>
                                </div>
                                <div class="font-bold ${t.type === 'income' ? 'text-emerald-400' : 'text-amber-400'}">
                                    ${t.type === 'income' ? '+' : '-'}${formatMoney(t.amount)}
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>

                <div class="mt-4 pt-3 border-t border-emerald-900/20 flex items-center justify-between">
                    <button onclick="openAddTxModal('${dateStr}')" class="text-xs text-emerald-400 font-semibold hover:underline flex items-center gap-1">
                        <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
                        <span>Add entry</span>
                    </button>
                    <button onclick="state.resetDemo()" class="text-[10px] text-muted hover:text-current">Load demo data</button>
                </div>
            `;
        }

        // Render Overview Charts via Chart.js
        function initOverviewCharts() {
            // Flow line chart
            const flowCtx = document.getElementById('overviewFlowChart');
            if (flowCtx) {
                new Chart(flowCtx, {
                    type: 'line',
                    data: {
                        labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
                        datasets: [
                            {
                                label: 'Income',
                                data: [12000, 15000, 14000, 17500, 16000, 18300],
                                borderColor: '#22c55e',
                                backgroundColor: 'rgba(34, 197, 94, 0.1)',
                                fill: true,
                                tension: 0.4
                            },
                            {
                                label: 'Expenses',
                                data: [7000, 8200, 6800, 7500, 6900, 5970],
                                borderColor: '#f59e0b',
                                backgroundColor: 'transparent',
                                borderDash: [4, 4],
                                tension: 0.4
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { display: false } },
                        scales: {
                            x: { grid: { display: false } },
                            y: { grid: { color: 'rgba(255, 255, 255, 0.05)' } }
                        }
                    }
                });
            }

            // Expense Donut
            const donutCtx = document.getElementById('expenseDonutChart');
            if (donutCtx) {
                const expCategories = {};
                state.data.transactions.filter(t => t.type === 'expense').forEach(t => {
                    expCategories[t.category] = (expCategories[t.category] || 0) + Number(t.amount);
                });

                new Chart(donutCtx, {
                    type: 'doughnut',
                    data: {
                        labels: Object.keys(expCategories),
                        datasets: [{
                            data: Object.values(expCategories),
                            backgroundColor: ['#22c55e', '#f59e0b', '#3b82f6', '#a855f7', '#ec4899', '#14b8a6'],
                            borderWidth: 0
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { display: false } },
                        cutout: '70%'
                    }
                });
            }
        }

        // ==========================================
        // PAGE 2: TRANSACTIONS (MONEY MOVES)
        // ==========================================
        function renderTransactionsPage() {
            let list = state.data.transactions;

            if (state.activeTxFilter !== 'all') {
                list = list.filter(t => t.type === state.activeTxFilter);
            }
            if (state.txCategoryFilter !== 'all') {
                list = list.filter(t => t.category === state.txCategoryFilter);
            }
            if (state.txSearchQuery) {
                const q = state.txSearchQuery.toLowerCase();
                list = list.filter(t => t.category.toLowerCase().includes(q) || (t.description || '').toLowerCase().includes(q));
            }

            const categories = Array.from(new Set(state.data.transactions.map(t => t.category)));

            return `
            <div class="space-y-6 pb-12">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <span class="text-xs font-bold tracking-widest text-emerald-400 uppercase">MONEY MOVES</span>
                        <h1 class="text-2xl sm:text-3xl font-extrabold text-current mt-0.5">Transactions</h1>
                        <p class="text-xs sm:text-sm text-muted mt-1">Keep every earning and expense in view.</p>
                    </div>
                    <button onclick="openAddTxModal()" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-4 py-2.5 rounded-xl shadow-lg transition-all flex items-center gap-2 text-sm">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
                        <span>Add transaction</span>
                    </button>
                </div>

                <!-- Filters Bar -->
                <div class="app-card p-4 rounded-2xl border flex flex-col md:flex-row items-center justify-between gap-4">
                    <!-- Segmented Tabs -->
                    <div class="flex items-center subtle-bg rounded-xl p-1 border border-emerald-900/30 w-full md:w-auto">
                        <button onclick="setTxFilter('all')" class="flex-1 md:flex-none px-4 py-1.5 rounded-lg text-xs font-semibold transition-colors ${state.activeTxFilter === 'all' ? 'bg-emerald-500 text-black' : 'text-muted hover:text-current'}">All</button>
                        <button onclick="setTxFilter('income')" class="flex-1 md:flex-none px-4 py-1.5 rounded-lg text-xs font-semibold transition-colors ${state.activeTxFilter === 'income' ? 'bg-emerald-500 text-black' : 'text-muted hover:text-current'}">Earnings</button>
                        <button onclick="setTxFilter('expense')" class="flex-1 md:flex-none px-4 py-1.5 rounded-lg text-xs font-semibold transition-colors ${state.activeTxFilter === 'expense' ? 'bg-emerald-500 text-black' : 'text-muted hover:text-current'}">Spending</button>
                    </div>

                    <!-- Search & Category Filters -->
                    <div class="flex flex-col sm:flex-row items-center gap-3 w-full md:w-auto">
                        <div class="relative w-full sm:w-64">
                            <input type="text" oninput="handleTxSearch(this.value)" value="${state.txSearchQuery}" placeholder="Search transactions..." class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2 pl-9 text-xs text-current focus:outline-none focus:border-emerald-500">
                            <svg class="w-4 h-4 text-muted absolute left-3 top-2.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>
                        </div>

                        <select onchange="handleTxCatFilter(this.value)" class="w-full sm:w-auto bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-3 py-2 text-xs text-current focus:outline-none focus:border-emerald-500">
                            <option value="all">All Categories</option>
                            ${categories.map(c => `<option value="${c}" ${state.txCategoryFilter === c ? 'selected' : ''}>${c}</option>`).join('')}
                        </select>
                    </div>
                </div>

                <!-- Transaction List -->
                <div class="app-card rounded-2xl border overflow-hidden">
                    <div class="divide-y divide-emerald-900/20">
                        ${list.length === 0 ? `
                            <div class="p-12 text-center text-muted text-xs space-y-3">
                                <p>No transaction records found matching your filters.</p>
                                <button onclick="openAddTxModal()" class="text-emerald-400 font-semibold hover:underline">+ Add your first transaction</button>
                            </div>
                        ` : list.map(t => `
                            <div class="p-4 flex items-center justify-between hover:bg-emerald-500/5 transition-colors">
                                <div class="flex items-center gap-4">
                                    <div class="w-10 h-10 rounded-xl bg-emerald-500/10 flex items-center justify-center border border-emerald-500/20">
                                        ${getCategoryIcon(t.category)}
                                    </div>
                                    <div>
                                        <div class="text-sm font-bold text-current">${t.category}</div>
                                        <div class="text-xs text-muted">${t.description || 'No description'}</div>
                                    </div>
                                </div>

                                <div class="flex items-center gap-6">
                                    <div class="text-right">
                                        <div class="text-sm font-bold ${t.type === 'income' ? 'text-emerald-400' : 'text-amber-400'}">
                                            ${t.type === 'income' ? '+' : '-'}${formatMoney(t.amount)}
                                        </div>
                                        <div class="text-xs text-muted">${t.date}</div>
                                    </div>

                                    <div class="flex items-center gap-2">
                                        <button onclick="openEditTxModal('${t.id}')" title="Edit" class="text-muted hover:text-emerald-400 p-1.5 rounded-lg transition-colors">
                                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/></svg>
                                        </button>
                                        <button onclick="deleteTx('${t.id}')" title="Delete" class="text-muted hover:text-red-400 p-1.5 rounded-lg transition-colors">
                                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/></svg>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            </div>
            `;
        }

        function setTxFilter(filter) {
            state.activeTxFilter = filter;
            renderApp();
        }
        function handleTxSearch(val) {
            state.txSearchQuery = val;
            renderApp();
        }
        function handleTxCatFilter(cat) {
            state.txCategoryFilter = cat;
            renderApp();
        }

        function deleteTx(id) {
            state.data.transactions = state.data.transactions.filter(t => t.id !== id);
            state.save();
            showToast("Transaction removed");
        }

        // ==========================================
        // PAGE 3: SAVINGS (YOUR SAFETY NET)
        // ==========================================
        function renderSavingsPage() {
            const calcs = state.getCalculations();
            const savings = state.data.savings;
            const pct = Math.min(100, Math.round((savings.balance / savings.target) * 100));

            return `
            <div class="space-y-6 pb-12">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <span class="text-xs font-bold tracking-widest text-emerald-400 uppercase">YOUR SAFETY NET</span>
                        <h1 class="text-2xl sm:text-3xl font-extrabold text-current mt-0.5">Savings</h1>
                        <p class="text-xs sm:text-sm text-muted mt-1">A separate balance for the months that ask more of you.</p>
                    </div>
                    <button onclick="openSavingsModal()" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-4 py-2.5 rounded-xl shadow-lg transition-all flex items-center gap-2 text-sm">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"/></svg>
                        <span>Manage savings</span>
                    </button>
                </div>

                <!-- Hero Savings Banner -->
                <div class="app-card p-8 rounded-3xl border bg-gradient-to-r from-emerald-950 via-brand-cardEmerald to-emerald-950 relative overflow-hidden flex flex-col md:flex-row items-center justify-between gap-8 border-emerald-500/30">
                    <div class="space-y-3 max-w-md">
                        <span class="text-xs font-bold tracking-widest text-emerald-400 uppercase">CURRENT SAVINGS BALANCE</span>
                        <div class="text-4xl sm:text-5xl font-extrabold text-white tracking-tight">${formatMoney(savings.balance)}</div>
                        <p class="text-xs text-emerald-300/80">Manually managed · never auto-transferred</p>
                    </div>

                    <!-- Circular Progress Gauge -->
                    <div class="relative w-36 h-36 flex items-center justify-center">
                        <svg class="w-full h-full transform -rotate-90" viewBox="0 0 36 36">
                            <path class="text-emerald-950" stroke-width="3.5" stroke="currentColor" fill="none" d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"/>
                            <path class="text-emerald-400" stroke-dasharray="${pct}, 100" stroke-width="3.5" stroke-linecap="round" stroke="currentColor" fill="none" d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"/>
                        </svg>
                        <div class="absolute text-center">
                            <div class="text-xl font-extrabold text-white">${pct}%</div>
                            <div class="text-[9px] uppercase font-bold text-emerald-300">Target ${formatMoney(savings.target)}</div>
                        </div>
                    </div>
                </div>

                <!-- Bottom Split: Safety net progress & Quick Actions -->
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Safety net progress -->
                    <div class="lg:col-span-7 app-card p-6 rounded-2xl border flex flex-col justify-between">
                        <div>
                            <h3 class="text-base font-bold text-current">Safety net progress</h3>
                            <p class="text-xs text-muted mb-4">Every bit worth breathing room</p>

                            <div class="space-y-3">
                                <div class="flex items-center justify-between text-xs font-semibold">
                                    <span>Saved: ${formatMoney(savings.balance)}</span>
                                    <span class="text-muted">Target: ${formatMoney(savings.target)}</span>
                                </div>
                                <div class="w-full bg-emerald-950/50 rounded-full h-3 overflow-hidden border border-emerald-900/30">
                                    <div class="bg-gradient-to-r from-emerald-500 to-mint h-full rounded-full" style="width: ${pct}%"></div>
                                </div>
                            </div>
                        </div>

                        <!-- Milestones -->
                        <div class="grid grid-cols-3 gap-2 mt-6 pt-4 border-t border-emerald-900/20 text-center">
                            <div class="p-2 rounded-xl subtle-bg border ${savings.balance >= 1000 ? 'border-emerald-500/40 text-emerald-400 font-bold' : 'border-emerald-900/20 text-muted'}">
                                <div class="text-[10px] uppercase">First ₹1,000</div>
                                <div class="text-xs mt-1">✓ Reached</div>
                            </div>
                            <div class="p-2 rounded-xl subtle-bg border ${savings.balance >= 5000 ? 'border-emerald-500/40 text-emerald-400 font-bold' : 'border-emerald-900/20 text-muted'}">
                                <div class="text-[10px] uppercase">1-week buffer</div>
                                <div class="text-xs mt-1">${savings.balance >= 5000 ? '✓ Active' : 'In progress'}</div>
                            </div>
                            <div class="p-2 rounded-xl subtle-bg border ${savings.balance >= 20000 ? 'border-emerald-500/40 text-emerald-400 font-bold' : 'border-emerald-900/20 text-muted'}">
                                <div class="text-[10px] uppercase">1-month buffer</div>
                                <div class="text-xs mt-1">${savings.balance >= 20000 ? '✓ Active' : 'Target'}</div>
                            </div>
                        </div>
                    </div>

                    <!-- Quick Actions -->
                    <div class="lg:col-span-5 app-card p-6 rounded-2xl border flex flex-col justify-between">
                        <div>
                            <h3 class="text-base font-bold text-current mb-1">Quick Actions</h3>
                            <p class="text-xs text-muted mb-6">Move money with intention</p>

                            <div class="space-y-3">
                                <button onclick="openSavingsModal('deposit')" class="w-full bg-emerald-500 hover:bg-emerald-600 text-black font-semibold py-3 px-4 rounded-xl shadow transition-all flex items-center justify-between text-xs">
                                    <span>+ Add money to savings</span>
                                    <span>&rarr;</span>
                                </button>
                                <button onclick="openSavingsModal('withdraw')" class="w-full bg-emerald-950/60 hover:bg-emerald-900/60 text-emerald-300 border border-emerald-800/40 font-semibold py-3 px-4 rounded-xl transition-all flex items-center justify-between text-xs">
                                    <span>- Withdraw from savings</span>
                                    <span>&rarr;</span>
                                </button>
                            </div>
                        </div>

                        <div class="text-[11px] text-muted flex items-center gap-2 mt-6">
                            <svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                            <span>Savings transfers do not modify income or expense totals.</span>
                        </div>
                    </div>
                </div>

                <!-- Savings History List -->
                <div class="app-card p-6 rounded-2xl border">
                    <h3 class="text-base font-bold text-current mb-4">Savings history</h3>
                    <div class="space-y-3">
                        ${savings.history.length === 0 ? `
                            <div class="text-xs text-muted text-center py-6">No savings transfers recorded yet.</div>
                        ` : savings.history.map(item => `
                            <div class="flex items-center justify-between p-3 rounded-xl subtle-bg border border-emerald-900/10 text-xs">
                                <div class="flex items-center gap-3">
                                    <div class="w-8 h-8 rounded-lg ${item.type === 'deposit' ? 'bg-emerald-500/10 text-emerald-400' : 'bg-amber-500/10 text-amber-400'} flex items-center justify-center font-bold">
                                        ${item.type === 'deposit' ? '+' : '-'}
                                    </div>
                                    <div>
                                        <div class="font-bold text-current capitalize">${item.type === 'deposit' ? 'Added to savings' : 'Withdrawn from savings'}</div>
                                        <div class="text-[10px] text-muted">${item.note || 'No note'}</div>
                                    </div>
                                </div>
                                <div class="text-right">
                                    <div class="font-bold ${item.type === 'deposit' ? 'text-emerald-400' : 'text-amber-400'}">
                                        ${item.type === 'deposit' ? '+' : '-'}${formatMoney(item.amount)}
                                    </div>
                                    <div class="text-[10px] text-muted">${item.date}</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            </div>
            `;
        }

        // ==========================================
        // PAGE 4: FINANCIAL INTELLIGENCE
        // ==========================================
        function renderIntelligencePage() {
            const calcs = state.getCalculations();

            return `
            <div class="space-y-6 pb-12">
                <div>
                    <span class="text-xs font-bold tracking-widest text-emerald-400 uppercase">CLARITY FOR THE UNPREDICTABLE</span>
                    <h1 class="text-2xl sm:text-3xl font-extrabold text-current mt-0.5">Financial intelligence</h1>
                    <p class="text-xs sm:text-sm text-muted mt-1">Signals from your real records — never made-up certainty.</p>
                </div>

                <!-- Stability Signal Banner -->
                <div class="app-card p-6 rounded-2xl border bg-gradient-to-r from-emerald-950 via-brand-cardEmerald to-emerald-950 border-emerald-500/40 flex flex-col md:flex-row items-center justify-between gap-4">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 rounded-2xl bg-emerald-500/20 border border-emerald-500/40 text-emerald-400 flex items-center justify-center font-bold text-lg">
                            ⚡
                        </div>
                        <div>
                            <span class="text-[10px] font-bold uppercase tracking-wider text-emerald-400">YOUR STABILITY SIGNAL</span>
                            <h2 class="text-lg font-bold text-white">Your earning rhythm is looking healthy.</h2>
                            <p class="text-xs text-emerald-200/70 mt-0.5">Your records show enough consistency to make a useful estimate for next month.</p>
                        </div>
                    </div>
                    <button onclick="setActiveTab('transactions')" class="text-xs text-emerald-400 font-semibold hover:underline flex items-center gap-1">
                        <span>Based on your data</span>
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
                    </button>
                </div>

                <!-- 3 Key Analysis Cards -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <!-- Income Pattern -->
                    <div class="app-card p-6 rounded-2xl border space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="text-xs uppercase font-bold text-muted tracking-wider">INCOME PATTERN</span>
                        </div>
                        <div>
                            <div class="text-2xl font-bold text-current">${formatMoney(calcs.avgDailyIncome)}</div>
                            <div class="text-xs text-muted">Average daily income</div>
                        </div>
                        <div class="pt-3 border-t border-emerald-900/20 text-xs space-y-2">
                            <div class="flex justify-between text-muted">
                                <span>Best day</span>
                                <span class="font-semibold text-emerald-400">Wednesday (${formatMoney(4300)})</span>
                            </div>
                            <div class="flex justify-between text-muted">
                                <span>Consistency</span>
                                <span class="font-semibold text-emerald-400">Moderate-High</span>
                            </div>
                        </div>
                    </div>

                    <!-- Income Forecast -->
                    <div class="app-card p-6 rounded-2xl border space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="text-xs uppercase font-bold text-muted tracking-wider">INCOME FORECAST</span>
                        </div>
                        <div>
                            <div class="text-2xl font-bold text-emerald-400">${formatMoney(Math.round(calcs.totalIncome * 0.95))}</div>
                            <div class="text-xs text-muted">Estimated next month income</div>
                        </div>
                        <p class="text-[11px] text-muted pt-3 border-t border-emerald-900/20 leading-relaxed">
                            Prediction based on recorded rhythm · not a guarantee.
                        </p>
                    </div>

                    <!-- Lean Month Check -->
                    <div class="app-card p-6 rounded-2xl border space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="text-xs uppercase font-bold text-muted tracking-wider">LEAN MONTH CHECK</span>
                        </div>
                        <div>
                            <div class="text-xl font-bold text-emerald-400">No gap detected</div>
                            <div class="text-xs text-muted">Expected income covers essential expenses</div>
                        </div>
                        <p class="text-[11px] text-muted pt-3 border-t border-emerald-900/20 leading-relaxed">
                            Your current balance covers predicted baseline food & fuel.
                        </p>
                    </div>
                </div>

                <!-- 3 Financial Scenarios -->
                <div class="app-card p-6 rounded-2xl border">
                    <div class="mb-6">
                        <span class="text-xs uppercase font-bold text-muted tracking-wider">PLAN FOR SWINGS, NOT AVERAGES</span>
                        <h3 class="text-lg font-bold text-current mt-0.5">What could next month feel like?</h3>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <!-- Lower than usual -->
                        <div class="p-4 rounded-xl subtle-bg border border-amber-500/20 space-y-2">
                            <div class="text-xs uppercase font-bold text-amber-400">Lower than usual</div>
                            <div class="text-xl font-extrabold text-current">${formatMoney(Math.round(calcs.totalIncome * 0.6))}</div>
                            <p class="text-xs text-muted leading-relaxed">Protect essentials first. Delay non-work spending.</p>
                        </div>

                        <!-- Normal rhythm -->
                        <div class="p-4 rounded-xl subtle-bg border border-emerald-500/30 space-y-2">
                            <div class="text-xs uppercase font-bold text-emerald-400">Normal rhythm</div>
                            <div class="text-xl font-extrabold text-current">${formatMoney(calcs.totalIncome)}</div>
                            <p class="text-xs text-muted leading-relaxed">Your current rhythm. Maintain steady buffer allocation.</p>
                        </div>

                        <!-- Better than usual -->
                        <div class="p-4 rounded-xl subtle-bg border border-blue-500/20 space-y-2">
                            <div class="text-xs uppercase font-bold text-blue-400">Better than usual</div>
                            <div class="text-xl font-extrabold text-current">${formatMoney(Math.round(calcs.totalIncome * 1.3))}</div>
                            <p class="text-xs text-muted leading-relaxed">Move extra straight to safety net buffer.</p>
                        </div>
                    </div>
                </div>
            </div>
            `;
        }

        // ==========================================
        // PAGE 5: SETTINGS (CONTROL ROOM)
        // ==========================================
        function renderSettingsPage() {
            const user = state.data.user;

            return `
            <div class="space-y-6 pb-12">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <span class="text-xs font-bold tracking-widest text-emerald-400 uppercase">YOUR CONTROL ROOM</span>
                        <h1 class="text-2xl sm:text-3xl font-extrabold text-current mt-0.5">Settings</h1>
                        <p class="text-xs sm:text-sm text-muted mt-1">Make STABIFLOW feel like yours.</p>
                    </div>
                    <button onclick="exportCSV()" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-4 py-2.5 rounded-xl shadow-lg transition-all flex items-center gap-2 text-sm">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg>
                        <span>Export CSV</span>
                    </button>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Profile Information -->
                    <div class="lg:col-span-6 app-card p-6 rounded-2xl border space-y-6">
                        <div class="flex items-center justify-between pb-4 border-b border-emerald-900/20">
                            <div class="flex items-center gap-3">
                                <div class="w-10 h-10 rounded-xl bg-emerald-500/20 text-emerald-400 flex items-center justify-center font-bold">
                                    ${user.name.charAt(0)}
                                </div>
                                <div>
                                    <h3 class="text-base font-bold text-current">Profile Information</h3>
                                    <p class="text-xs text-muted">This is how your workspace knows you.</p>
                                </div>
                            </div>
                        </div>

                        <form onsubmit="saveProfileSettings(event)" class="space-y-4">
                            <div>
                                <label class="block text-xs font-semibold text-muted uppercase mb-1">Full name</label>
                                <input type="text" id="settingName" value="${user.name}" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2.5 text-xs text-current focus:outline-none focus:border-emerald-500">
                            </div>

                            <div>
                                <label class="block text-xs font-semibold text-muted uppercase mb-1">Occupation</label>
                                <input type="text" id="settingOccupation" value="${user.occupation}" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2.5 text-xs text-current focus:outline-none focus:border-emerald-500">
                            </div>

                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-xs font-semibold text-muted uppercase mb-1">Currency</label>
                                    <select id="settingCurrency" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-3 py-2.5 text-xs text-current focus:outline-none focus:border-emerald-500">
                                        <option value="INR" ${user.currency === 'INR' ? 'selected' : ''}>INR - Indian Rupee</option>
                                        <option value="USD" ${user.currency === 'USD' ? 'selected' : ''}>USD - US Dollar</option>
                                        <option value="EUR" ${user.currency === 'EUR' ? 'selected' : ''}>EUR - Euro</option>
                                        <option value="GBP" ${user.currency === 'GBP' ? 'selected' : ''}>GBP - British Pound</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs font-semibold text-muted uppercase mb-1">Main income source</label>
                                    <input type="text" id="settingIncomeSource" value="${user.incomeSource}" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2.5 text-xs text-current focus:outline-none focus:border-emerald-500">
                                </div>
                            </div>

                            <button type="submit" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-4 py-2 rounded-xl text-xs shadow transition-all">
                                Save Profile Changes
                            </button>
                        </form>
                    </div>

                    <!-- Preferences & Theme Selection -->
                    <div class="lg:col-span-6 space-y-6">
                        <div class="app-card p-6 rounded-2xl border space-y-4">
                            <h3 class="text-base font-bold text-current">Preferences</h3>
                            <div class="space-y-3">
                                <div class="flex items-center justify-between p-3 rounded-xl subtle-bg border border-emerald-900/20">
                                    <div>
                                        <div class="text-xs font-bold text-current">Weekly money digest</div>
                                        <div class="text-[10px] text-muted">A gentle summary every Monday morning</div>
                                    </div>
                                    <input type="checkbox" ${user.digestEnabled ? 'checked' : ''} onchange="toggleSetting('digestEnabled')" class="rounded border-emerald-900 text-emerald-500">
                                </div>

                                <div class="flex items-center justify-between p-3 rounded-xl subtle-bg border border-emerald-900/20">
                                    <div>
                                        <div class="text-xs font-bold text-current">Low balance alerts</div>
                                        <div class="text-[10px] text-muted">Get notified when your buffer dips</div>
                                    </div>
                                    <input type="checkbox" ${user.alertsEnabled ? 'checked' : ''} onchange="toggleSetting('alertsEnabled')" class="rounded border-emerald-900 text-emerald-500">
                                </div>
                            </div>

                            <!-- Workspace Mood (Theme Switcher) -->
                            <div class="pt-4 border-t border-emerald-900/20">
                                <label class="block text-xs font-semibold text-muted uppercase mb-2">Choose the workspace mood</label>
                                <div class="grid grid-cols-3 gap-2">
                                    <button onclick="setTheme('emerald')" class="p-3 rounded-xl border text-center text-xs font-bold transition-all ${state.data.theme === 'emerald' ? 'border-emerald-500 bg-emerald-500/20 text-emerald-400' : 'border-emerald-900/30 subtle-bg text-muted'}">
                                        🌲 Emerald
                                    </button>
                                    <button onclick="setTheme('noir')" class="p-3 rounded-xl border text-center text-xs font-bold transition-all ${state.data.theme === 'noir' ? 'border-emerald-500 bg-emerald-500/20 text-emerald-400' : 'border-emerald-900/30 subtle-bg text-muted'}">
                                        🌑 Noir
                                    </button>
                                    <button onclick="setTheme('light')" class="p-3 rounded-xl border text-center text-xs font-bold transition-all ${state.data.theme === 'light' ? 'border-emerald-600 bg-emerald-600/10 text-emerald-600' : 'border-emerald-900/30 subtle-bg text-muted'}">
                                        ☀️ Light
                                    </button>
                                </div>
                            </div>
                        </div>

                        <!-- Data Controls -->
                        <div class="app-card p-6 rounded-2xl border space-y-4">
                            <h3 class="text-base font-bold text-current">Workspace data controls</h3>
                            <div class="flex items-center gap-3">
                                <button onclick="state.resetDemo()" class="flex-1 bg-emerald-950/60 hover:bg-emerald-900/60 text-emerald-300 border border-emerald-800/40 text-xs font-semibold py-2.5 rounded-xl transition-all">
                                    Reload Demo Data
                                </button>
                                <button onclick="state.clearData()" class="flex-1 bg-red-950/40 hover:bg-red-900/40 text-red-400 border border-red-800/40 text-xs font-semibold py-2.5 rounded-xl transition-all">
                                    Clear All Data
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            `;
        }

        function saveProfileSettings(e) {
            e.preventDefault();
            state.data.user.name = document.getElementById('settingName').value;
            state.data.user.occupation = document.getElementById('settingOccupation').value;
            state.data.user.currency = document.getElementById('settingCurrency').value;
            state.data.user.incomeSource = document.getElementById('settingIncomeSource').value;
            state.save();
            showToast("Profile settings updated");
        }

        function toggleSetting(key) {
            state.data.user[key] = !state.data.user[key];
            state.save();
        }

        // ==========================================
        // MODALS ENGINE (TRANSACTIONS & SAVINGS)
        // ==========================================
        function renderModals() {
            if (!state.modalState) return '';

            if (state.modalState === 'addTx' || state.modalState === 'editTx') {
                const isEdit = state.modalState === 'editTx';
                const tx = isEdit ? state.data.transactions.find(t => t.id === state.editingTxId) : null;

                const defaultType = tx ? tx.type : 'income';
                const defaultCat = tx ? tx.category : 'Delivery';
                const defaultAmt = tx ? tx.amount : '';
                const defaultDate = tx ? tx.date : (state.selectedCalendarDate || getLocalDateString(new Date()));
                const defaultDesc = tx ? tx.description : '';

                return `
                <div class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/70 backdrop-blur-sm">
                    <div class="app-card w-full max-w-md p-6 rounded-3xl border border-emerald-500/40 shadow-2xl relative">
                        <div class="flex items-center justify-between mb-4">
                            <div>
                                <span class="text-[10px] font-bold uppercase tracking-wider text-emerald-400">MONEY MOVES</span>
                                <h3 class="text-xl font-bold text-current">${isEdit ? 'Edit transaction' : 'Add transaction'}</h3>
                            </div>
                            <button onclick="closeModal()" class="text-muted hover:text-current p-1">
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
                            </button>
                        </div>

                        <form onsubmit="handleTxFormSubmit(event, '${isEdit ? state.editingTxId : ''}')" class="space-y-4">
                            <!-- Type Segmented Selector -->
                            <div class="flex items-center subtle-bg p-1 rounded-xl border border-emerald-900/40">
                                <button type="button" onclick="setTxModalType('income')" id="btnTypeIncome" class="flex-1 py-2 rounded-lg text-xs font-bold transition-all ${defaultType === 'income' ? 'bg-emerald-500 text-black' : 'text-muted'}">I earned</button>
                                <button type="button" onclick="setTxModalType('expense')" id="btnTypeExpense" class="flex-1 py-2 rounded-lg text-xs font-bold transition-all ${defaultType === 'expense' ? 'bg-emerald-500 text-black' : 'text-muted'}">I spent</button>
                            </div>
                            <input type="hidden" id="modalTxType" value="${defaultType}">

                            <div>
                                <label class="block text-xs font-semibold text-muted uppercase mb-1">Amount</label>
                                <input type="number" id="modalTxAmount" required value="${defaultAmt}" placeholder="0" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2.5 text-sm font-bold text-current focus:outline-none focus:border-emerald-500">
                            </div>

                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="block text-xs font-semibold text-muted uppercase mb-1">Category</label>
                                    <select id="modalTxCategory" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-3 py-2.5 text-xs text-current focus:outline-none focus:border-emerald-500">
                                        <option value="Delivery" ${defaultCat === 'Delivery' ? 'selected' : ''}>Delivery</option>
                                        <option value="Cab driving" ${defaultCat === 'Cab driving' ? 'selected' : ''}>Cab driving</option>
                                        <option value="Freelancing" ${defaultCat === 'Freelancing' ? 'selected' : ''}>Freelancing</option>
                                        <option value="Salary" ${defaultCat === 'Salary' ? 'selected' : ''}>Salary</option>
                                        <option value="Fuel" ${defaultCat === 'Fuel' ? 'selected' : ''}>Fuel</option>
                                        <option value="Food" ${defaultCat === 'Food' ? 'selected' : ''}>Food</option>
                                        <option value="Vehicle maintenance" ${defaultCat === 'Vehicle maintenance' ? 'selected' : ''}>Vehicle maintenance</option>
                                        <option value="Rent" ${defaultCat === 'Rent' ? 'selected' : ''}>Rent</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs font-semibold text-muted uppercase mb-1">Date</label>
                                    <input type="date" id="modalTxDate" required value="${defaultDate}" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-3 py-2 text-xs text-current focus:outline-none focus:border-emerald-500">
                                </div>
                            </div>

                            <div>
                                <label class="block text-xs font-semibold text-muted uppercase mb-1">Description (Optional)</label>
                                <input type="text" id="modalTxDesc" value="${defaultDesc}" placeholder="What was this for?" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2 text-xs text-current focus:outline-none focus:border-emerald-500">
                            </div>

                            <div class="pt-4 flex items-center justify-end gap-3">
                                <button type="button" onclick="closeModal()" class="px-4 py-2 rounded-xl text-xs font-semibold text-muted hover:text-current">Cancel</button>
                                <button type="submit" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-5 py-2.5 rounded-xl shadow text-xs">Save transaction &rarr;</button>
                            </div>
                        </form>
                    </div>
                </div>
                `;
            }

            if (state.modalState === 'savingsModal') {
                return `
                <div class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/70 backdrop-blur-sm">
                    <div class="app-card w-full max-w-md p-6 rounded-3xl border border-emerald-500/40 shadow-2xl relative">
                        <div class="flex items-center justify-between mb-4">
                            <div>
                                <span class="text-[10px] font-bold uppercase tracking-wider text-emerald-400">SAVINGS BALANCE</span>
                                <h3 class="text-xl font-bold text-current">Move money intentionally</h3>
                            </div>
                            <button onclick="closeModal()" class="text-muted hover:text-current p-1">
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
                            </button>
                        </div>

                        <form onsubmit="handleSavingsFormSubmit(event)" class="space-y-4">
                            <div class="flex items-center subtle-bg p-1 rounded-xl border border-emerald-900/40">
                                <button type="button" onclick="setSavingsModalAction('deposit')" id="btnSavDeposit" class="flex-1 py-2 rounded-lg text-xs font-bold bg-emerald-500 text-black transition-all">Add money</button>
                                <button type="button" onclick="setSavingsModalAction('withdraw')" id="btnSavWithdraw" class="flex-1 py-2 rounded-lg text-xs font-bold text-muted transition-all">Withdraw</button>
                            </div>
                            <input type="hidden" id="modalSavingsAction" value="deposit">

                            <div>
                                <label class="block text-xs font-semibold text-muted uppercase mb-1">Amount</label>
                                <input type="number" id="modalSavingsAmount" required placeholder="500" class="w-full bg-emerald-950/20 border border-emerald-900/40 rounded-xl px-4 py-2.5 text-sm font-bold text-current focus:outline-none focus:border-emerald-500">
                            </div>

                            <div class="text-[11px] text-muted flex items-center gap-2">
                                <svg class="w-4 h-4 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                                <span>This does not change income or expenses.</span>
                            </div>

                            <div class="pt-4 flex items-center justify-end gap-3">
                                <button type="button" onclick="closeModal()" class="px-4 py-2 rounded-xl text-xs font-semibold text-muted hover:text-current">Cancel</button>
                                <button type="submit" id="btnSavingsSubmit" class="bg-emerald-500 hover:bg-emerald-600 text-black font-semibold px-5 py-2.5 rounded-xl shadow text-xs">Add to savings</button>
                            </div>
                        </form>
                    </div>
                </div>
                `;
            }

            return '';
        }

        function setTxModalType(type) {
            document.getElementById('modalTxType').value = type;
            const bInc = document.getElementById('btnTypeIncome');
            const bExp = document.getElementById('btnTypeExpense');

            if (type === 'income') {
                bInc.className = 'flex-1 py-2 rounded-lg text-xs font-bold bg-emerald-500 text-black transition-all';
                bExp.className = 'flex-1 py-2 rounded-lg text-xs font-bold text-muted transition-all';
            } else {
                bExp.className = 'flex-1 py-2 rounded-lg text-xs font-bold bg-emerald-500 text-black transition-all';
                bInc.className = 'flex-1 py-2 rounded-lg text-xs font-bold text-muted transition-all';
            }
        }

        function setSavingsModalAction(action) {
            document.getElementById('modalSavingsAction').value = action;
            const bDep = document.getElementById('btnSavDeposit');
            const bWit = document.getElementById('btnSavWithdraw');
            const btnSub = document.getElementById('btnSavingsSubmit');

            if (action === 'deposit') {
                bDep.className = 'flex-1 py-2 rounded-lg text-xs font-bold bg-emerald-500 text-black transition-all';
                bWit.className = 'flex-1 py-2 rounded-lg text-xs font-bold text-muted transition-all';
                btnSub.innerText = 'Add to savings';
            } else {
                bWit.className = 'flex-1 py-2 rounded-lg text-xs font-bold bg-emerald-500 text-black transition-all';
                bDep.className = 'flex-1 py-2 rounded-lg text-xs font-bold text-muted transition-all';
                btnSub.innerText = 'Withdraw funds';
            }
        }

        function handleTxFormSubmit(e, editId) {
            e.preventDefault();
            const type = document.getElementById('modalTxType').value;
            const amount = Number(document.getElementById('modalTxAmount').value);
            const category = document.getElementById('modalTxCategory').value;
            const date = document.getElementById('modalTxDate').value;
            const description = document.getElementById('modalTxDesc').value;

            if (editId) {
                const tx = state.data.transactions.find(t => t.id === editId);
                if (tx) {
                    tx.type = type;
                    tx.amount = amount;
                    tx.category = category;
                    tx.date = date;
                    tx.description = description;
                }
                showToast("Transaction updated");
            } else {
                state.data.transactions.unshift({
                    id: 't_' + Date.now(),
                    type,
                    amount,
                    category,
                    date,
                    description
                });
                showToast("Transaction added");
            }
            closeModal();
            state.save();
        }

        function handleSavingsFormSubmit(e) {
            e.preventDefault();
            const action = document.getElementById('modalSavingsAction').value;
            const amount = Number(document.getElementById('modalSavingsAmount').value);

            if (action === 'deposit') {
                state.data.savings.balance += amount;
                state.data.savings.history.unshift({
                    id: 's_' + Date.now(),
                    type: 'deposit',
                    amount,
                    date: new Date().toISOString().slice(0, 10),
                    note: 'Added to savings'
                });
                showToast("Savings updated");
            } else {
                if (amount > state.data.savings.balance) {
                    showToast("Cannot withdraw more than current savings balance");
                    return;
                }
                state.data.savings.balance -= amount;
                state.data.savings.history.unshift({
                    id: 's_' + Date.now(),
                    type: 'withdraw',
                    amount,
                    date: new Date().toISOString().slice(0, 10),
                    note: 'Withdrawn from savings'
                });
                showToast("Withdrawal recorded");
            }
            closeModal();
            state.save();
        }

        function openAddTxModal(defaultDate) {
            if (defaultDate) state.selectedCalendarDate = defaultDate;
            state.modalState = 'addTx';
            state.editingTxId = null;
            renderApp();
        }

        function openEditTxModal(id) {
            state.modalState = 'editTx';
            state.editingTxId = id;
            renderApp();
        }

        function openSavingsModal(action = 'deposit') {
            state.modalState = 'savingsModal';
            renderApp();
            setTimeout(() => setSavingsModalAction(action), 10);
        }

        function closeModal() {
            state.modalState = null;
            state.editingTxId = null;
            renderApp();
        }

        // ==========================================
        // ACTION CONTROLLERS & INTERACTION HANDLERS
        // ==========================================
        function setActiveTab(tab) {
            state.activeTab = tab;
            renderApp();
        }

        function setTheme(theme) {
            state.data.theme = theme;
            state.applyTheme();
            state.save();
        }

        function toggleMobileSidebar() {
            const sidebar = document.getElementById('mainSidebar');
            if (sidebar) {
                sidebar.classList.toggle('-translate-x-full');
            }
        }

        function toggleNotifications() {
            state.notificationsOpen = !state.notificationsOpen;
            renderApp();
        }

        function markAllNotificationsRead() {
            state.notifications.forEach(n => n.read = true);
            state.notificationsOpen = false;
            renderApp();
            showToast("Notifications marked as read");
        }

        function handleLogout() {
            state.data.isAuthenticated = false;
            state.save();
            showToast("Signed out of workspace");
        }

        // ==========================================
        // MAIN APPLICATION RENDER ENGINE
        // ==========================================
        function renderApp() {
            const app = document.getElementById('app');
            if (!app) return;

            // Apply global CSS theme class
            state.applyTheme();

            if (!state.data.isAuthenticated) {
                app.innerHTML = renderAuthScreen();
                return;
            }

            let pageContent = '';
            switch (state.activeTab) {
                case 'overview':
                    pageContent = renderOverviewPage();
                    break;
                case 'transactions':
                    pageContent = renderTransactionsPage();
                    break;
                case 'savings':
                    pageContent = renderSavingsPage();
                    break;
                case 'intelligence':
                    pageContent = renderIntelligencePage();
                    break;
                case 'settings':
                    pageContent = renderSettingsPage();
                    break;
                default:
                    pageContent = renderOverviewPage();
            }

            app.innerHTML = `
                ${renderSidebar()}
                <div class="md:pl-64 flex flex-col flex-1 min-h-screen">
                    ${renderHeader()}
                    <main class="flex-1 p-4 sm:p-6 lg:p-8 max-w-7xl w-full mx-auto">
                        ${pageContent}
                    </main>
                </div>
                ${renderModals()}
            `;

            // Post-render attachments (Calendar rendering & Chart.js initialization)
            if (state.activeTab === 'overview') {
                renderCalendar();
                setTimeout(() => initOverviewCharts(), 50);
            }
        }

        // ==========================================
        // INIT ON WINDOW LOAD
        // ==========================================
        window.onload = function () {
            renderApp();
        };
    </script>
</body>
</html>
