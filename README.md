# Brand-dashboard
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enabler E-Commerce Dashboard - Thailand</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: { sans: ['Inter', 'sans-serif'] },
                    colors: {
                        shopee: '#ee4d2d',
                        lazada: '#0f146d',
                        tiktok: '#000000',
                        brand: '#3b82f6',
                        target: '#10b981'
                    }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #f8fafc; }
        .metric-card { transition: transform 0.2s ease-in-out; }
        .metric-card:hover { transform: translateY(-3px); }
        .scrollbar-hide::-webkit-scrollbar { display: none; }
        .scrollbar-hide { -ms-overflow-style: none; scrollbar-width: none; }
        .nav-link.active { background-color: #3b82f6; color: white; }
        .nav-link { transition: all 0.2s; }
        .sub-tab.active { border-color: #3b82f6; color: #3b82f6; font-weight: 600; }
    </style>
</head>
<body class="text-slate-800 h-screen flex overflow-hidden">

    <!-- Sidebar -->
    <aside class="w-64 bg-slate-900 text-white flex flex-col hidden md:flex z-20 shadow-xl">
        <div class="p-6 border-b border-slate-700">
            <h1 class="text-xl font-bold flex items-center gap-2">
                <i class="fa-solid fa-chart-line text-brand"></i>
                OmniEnable TH
            </h1>
            <p class="text-xs text-slate-400 mt-1">Brand Operations Center</p>
        </div>
        <nav class="flex-1 p-4 space-y-2">
            <button onclick="switchPage('page-overview', this)" class="nav-link active w-full flex items-center gap-3 px-4 py-3 rounded-lg font-medium text-left">
                <i class="fa-solid fa-bullseye w-5"></i> 1. Overview & Targets
            </button>
            <button onclick="switchPage('page-mechanics', this)" class="nav-link text-slate-300 hover:bg-slate-800 hover:text-white w-full flex items-center gap-3 px-4 py-3 rounded-lg font-medium text-left">
                <i class="fa-solid fa-rocket w-5"></i> 2. Marketing Mechanics
            </button>
            <button onclick="switchPage('page-deep-dive', this)" class="nav-link text-slate-300 hover:bg-slate-800 hover:text-white w-full flex items-center gap-3 px-4 py-3 rounded-lg font-medium text-left">
                <i class="fa-solid fa-chart-pie w-5"></i> 3. Channel Deep-Dive
            </button>
            <button onclick="switchPage('page-products', this)" class="nav-link text-slate-300 hover:bg-slate-800 hover:text-white w-full flex items-center gap-3 px-4 py-3 rounded-lg font-medium text-left">
                <i class="fa-solid fa-boxes-stacked w-5"></i> 4. Product & Category
            </button>
        </nav>
        <div class="p-4 border-t border-slate-700">
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center">
                    <i class="fa-solid fa-user text-sm"></i>
                </div>
                <div>
                    <p class="text-sm font-medium">Account Manager</p>
                    <p class="text-xs text-slate-400">admin@omnienable.com</p>
                </div>
            </div>
        </div>
    </aside>

    <!-- Main Content -->
    <main class="flex-1 flex flex-col h-screen overflow-y-auto relative">
        
        <!-- Top Header -->
        <header class="bg-white border-b border-slate-200 px-8 py-4 flex flex-col sm:flex-row justify-between items-center sticky top-0 z-10 gap-4 shadow-sm">
            <div class="flex items-center gap-4">
                <div class="relative">
                    <select id="brandSelector" onchange="updateBrandData()" class="appearance-none bg-slate-50 border border-slate-300 text-slate-700 py-2 pl-4 pr-10 rounded-lg focus:outline-none focus:ring-2 focus:ring-brand font-semibold">
                        <option value="cosmetics">Brand: Acme Cosmetics TH</option>
                        <option value="tech">Brand: TechGear Plus</option>
                    </select>
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-3 text-slate-500">
                        <i class="fa-solid fa-chevron-down text-xs"></i>
                    </div>
                </div>
            </div>
            
            <div class="flex items-center gap-4">
                <div class="bg-slate-100 text-sm font-medium px-4 py-2 rounded-lg flex items-center gap-2">
                    <i class="fa-regular fa-calendar"></i>
                    May 1 - May 28, 2026
                </div>
                <button class="bg-white border border-slate-300 hover:bg-slate-50 text-slate-700 px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                    <i class="fa-solid fa-download mr-1"></i> Export
                </button>
            </div>
        </header>

        <div class="p-8">
            <!-- ========================================== -->
            <!-- PAGE 1: OVERVIEW & TARGETS                 -->
            <!-- ========================================== -->
            <div id="page-overview" class="page-content block">
                <div class="mb-6 flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-2xl font-bold text-slate-800">Sales vs Target Pacing</h2>
                        <p class="text-slate-500 text-sm mt-1">Key e-commerce metrics compared against May 2026 goals.</p>
                    </div>
                    <div>
                        <button onclick="generateOverviewSummary()" class="bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-700 hover:to-indigo-700 text-white font-semibold py-2 px-4 rounded-lg shadow-sm flex items-center gap-2 transition-all">
                            <span>✨ Generate Executive Summary</span>
                        </button>
                    </div>
                </div>

                <!-- Target Metrics Grid -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
                    <!-- Sales vs Target -->
                    <div class="metric-card bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex justify-between items-start mb-2">
                            <p class="text-sm font-medium text-slate-500">Sales (GMV) vs Target</p>
                            <div class="bg-green-100 text-green-700 p-1.5 rounded-lg"><i class="fa-solid fa-baht-sign"></i></div>
                        </div>
                        <h3 id="overview-gmv" class="text-2xl font-bold text-slate-800 mb-1">฿1,425,000</h3>
                        <div class="flex justify-between text-xs text-slate-500 mb-2">
                            <span id="overview-gmv-target">Target: ฿1,500,000</span>
                            <span id="overview-gmv-pct" class="font-bold text-green-600">95%</span>
                        </div>
                        <div class="w-full bg-slate-100 rounded-full h-2">
                            <div id="overview-gmv-bar" class="bg-green-500 h-2 rounded-full" style="width: 95%"></div>
                        </div>
                    </div>
                    
                    <!-- Orders vs Target -->
                    <div class="metric-card bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex justify-between items-start mb-2">
                            <p class="text-sm font-medium text-slate-500">Orders vs Target</p>
                            <div class="bg-blue-100 text-blue-700 p-1.5 rounded-lg"><i class="fa-solid fa-box-open"></i></div>
                        </div>
                        <h3 id="overview-orders" class="text-2xl font-bold text-slate-800 mb-1">5,140</h3>
                        <div class="flex justify-between text-xs text-slate-500 mb-2">
                            <span id="overview-orders-target">Target: 6,000</span>
                            <span id="overview-orders-pct" class="font-bold text-blue-600">85%</span>
                        </div>
                        <div class="w-full bg-slate-100 rounded-full h-2">
                            <div id="overview-orders-bar" class="bg-blue-500 h-2 rounded-full" style="width: 85%"></div>
                        </div>
                    </div>

                    <!-- AOV vs Target -->
                    <div class="metric-card bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex justify-between items-start mb-2">
                            <p class="text-sm font-medium text-slate-500">AOV vs Target</p>
                            <div class="bg-orange-100 text-orange-700 p-1.5 rounded-lg"><i class="fa-solid fa-cart-shopping"></i></div>
                        </div>
                        <h3 id="overview-aov" class="text-2xl font-bold text-slate-800 mb-1">฿277</h3>
                        <div class="flex justify-between text-xs text-slate-500 mb-2">
                            <span id="overview-aov-target">Target: ฿250</span>
                            <span id="overview-aov-pct" class="font-bold text-orange-600">110%</span>
                        </div>
                        <div class="w-full bg-slate-100 rounded-full h-2">
                            <div id="overview-aov-bar" class="bg-orange-500 h-2 rounded-full" style="width: 100%"></div>
                        </div>
                    </div>

                    <!-- CR% vs Target -->
                    <div class="metric-card bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex justify-between items-start mb-2">
                            <p class="text-sm font-medium text-slate-500">Blended CR% vs Target</p>
                            <div class="bg-rose-100 text-rose-700 p-1.5 rounded-lg"><i class="fa-solid fa-bolt"></i></div>
                        </div>
                        <h3 id="overview-cr" class="text-2xl font-bold text-slate-800 mb-1">2.77%</h3>
                        <div class="flex justify-between text-xs text-slate-500 mb-2">
                            <span id="overview-cr-target">Target: 3.00%</span>
                            <span id="overview-cr-pct" class="font-bold text-rose-600">92%</span>
                        </div>
                        <div class="w-full bg-slate-100 rounded-full h-2">
                            <div id="overview-cr-bar" class="bg-rose-500 h-2 rounded-full" style="width: 92%"></div>
                        </div>
                    </div>
                </div>

                <!-- Summary Panel -->
                <div id="overviewSummaryBox" class="hidden mb-8 bg-gradient-to-r from-slate-50 to-blue-50 border border-blue-200 rounded-xl p-6 shadow-sm relative">
                    <button onclick="closeSummaryBox('overviewSummaryBox')" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                        <i class="fa-solid fa-xmark text-lg"></i>
                    </button>
                    <div class="flex items-start gap-4">
                        <div class="text-2xl text-blue-600 mt-1">
                            <i class="fa-solid fa-brain"></i>
                        </div>
                        <div class="flex-1">
                            <h4 class="font-bold text-slate-900 mb-2 flex items-center gap-2">
                                ✨ Executive Performance Summary (AI Pilot)
                            </h4>
                            <div id="overviewSummaryText" class="text-slate-700 text-sm space-y-2 whitespace-pre-wrap leading-relaxed">
                                Loading analysis...
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Daily Run-Rate & Daily Velocity KPI Scorecards -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                    <div class="bg-gradient-to-br from-indigo-500 to-indigo-600 text-white p-5 rounded-xl shadow-sm">
                        <p class="text-xs font-semibold text-indigo-100 uppercase tracking-wider">Pacing Target Attained</p>
                        <h4 id="runrate-pct-score" class="text-2xl font-bold mt-1">95.0%</h4>
                        <p class="text-xs text-indigo-100 mt-2">Target pacing MTD threshold</p>
                    </div>
                    <div class="bg-gradient-to-br from-emerald-500 to-emerald-600 text-white p-5 rounded-xl shadow-sm">
                        <p class="text-xs font-semibold text-emerald-100 uppercase tracking-wider">Remaining Target Balance</p>
                        <h4 id="runrate-rem-score" class="text-2xl font-bold mt-1">฿75,000</h4>
                        <p class="text-xs text-emerald-100 mt-2">Gap to hit monthly close goal</p>
                    </div>
                    <div class="bg-gradient-to-br from-blue-500 to-blue-600 text-white p-5 rounded-xl shadow-sm">
                        <p class="text-xs font-semibold text-blue-100 uppercase tracking-wider">Required Daily Velocity</p>
                        <h4 id="runrate-daily-req" class="text-2xl font-bold mt-1">฿25,000 / Day</h4>
                        <p class="text-xs text-blue-100 mt-2">For remaining 3 days of May</p>
                    </div>
                </div>

                <!-- Charts Section -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-8">
                    <!-- Chart 1: YoY Comparison May 2025 vs May 2026 -->
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-base font-bold text-slate-800">YoY Performance (May 2025 vs 2026)</h3>
                            <span class="text-xs font-semibold bg-green-100 text-green-700 px-2 py-1 rounded">YoY Target: +20% Growth</span>
                        </div>
                        <div class="relative h-72 w-full">
                            <canvas id="yoyGrowthChart"></canvas>
                        </div>
                    </div>

                    <!-- Chart 2: Daily Sales Actual vs Target (Non-cumulative, discrete) -->
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-base font-bold text-slate-800">Daily Sales vs Daily Target (Discrete)</h3>
                            <span class="text-xs font-semibold bg-blue-100 text-blue-700 px-2 py-1 rounded">Full Month Run-Rate</span>
                        </div>
                        <div class="relative h-72 w-full">
                            <canvas id="dailyVelocityChart"></canvas>
                        </div>
                    </div>
                </div>

                <!-- Platform Share & Core breakdown -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
                    <div class="lg:col-span-2 bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <h3 class="text-base font-bold text-slate-800 mb-4">Platform Channel Breakdown</h3>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="text-xs text-slate-500 uppercase border-b border-slate-200">
                                        <th class="py-3 font-semibold">Platform</th>
                                        <th class="py-3 text-right font-semibold">GMV</th>
                                        <th class="py-3 text-right font-semibold">Orders</th>
                                        <th class="py-3 text-right font-semibold">AOV</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td class="py-3 font-medium text-slate-800">Shopee TH</td>
                                        <td class="py-3 text-right text-slate-600">฿598,500</td>
                                        <td class="py-3 text-right text-slate-600">2,300</td>
                                        <td class="py-3 text-right text-slate-600">฿260</td>
                                    </tr>
                                    <tr>
                                        <td class="py-3 font-medium text-slate-800">Lazada TH</td>
                                        <td class="py-3 text-right text-slate-600">฿498,750</td>
                                        <td class="py-3 text-right text-slate-600">1,610</td>
                                        <td class="py-3 text-right text-slate-600">฿310</td>
                                    </tr>
                                    <tr>
                                        <td class="py-3 font-medium text-slate-800">TikTok Shop TH</td>
                                        <td class="py-3 text-right text-slate-600">฿327,750</td>
                                        <td class="py-3 text-right text-slate-600">1,230</td>
                                        <td class="py-3 text-right text-slate-600">฿266</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col">
                        <h3 class="text-base font-bold text-slate-800 mb-4">GMV Share by Platform</h3>
                        <div class="relative h-56 w-full flex-1 flex justify-center items-center">
                            <canvas id="platformShareChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>

            <!-- ========================================== -->
            <!-- PAGE 2: MECHANICS OVERVIEW                 -->
            <!-- ========================================== -->
            <div id="page-mechanics" class="page-content hidden">
                <div class="mb-6 flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-2xl font-bold text-slate-800">Marketing Mechanics & Drivers</h2>
                        <p class="text-slate-500 text-sm mt-1">Analyzing the impact of Livestreams, Paid Ads, and Affiliates on total GMV.</p>
                    </div>
                    <div>
                        <button onclick="generateMechanicsOptimization()" class="bg-gradient-to-r from-violet-600 to-indigo-600 hover:from-violet-700 hover:to-indigo-700 text-white font-semibold py-2 px-4 rounded-lg shadow-sm flex items-center gap-2 transition-all">
                            <span>✨ Optimize Marketing ROI</span>
                        </button>
                    </div>
                </div>

                <!-- Optimization Panel -->
                <div id="mechanicsSummaryBox" class="hidden mb-8 bg-gradient-to-r from-slate-50 to-violet-50 border border-violet-200 rounded-xl p-6 shadow-sm relative">
                    <button onclick="closeSummaryBox('mechanicsSummaryBox')" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                        <i class="fa-solid fa-xmark text-lg"></i>
                    </button>
                    <div class="flex items-start gap-4">
                        <div class="text-2xl text-violet-600 mt-1">
                            <i class="fa-solid fa-wand-magic-sparkles"></i>
                        </div>
                        <div class="flex-1">
                            <h4 class="font-bold text-slate-900 mb-2 flex items-center gap-2">
                                ✨ Marketing Optimization Plan (AI Pilot)
                            </h4>
                            <div id="mechanicsSummaryText" class="text-slate-700 text-sm space-y-2 whitespace-pre-wrap leading-relaxed">
                                Loading analysis...
                            </div>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-4 gap-4 mb-8">
                    <!-- Ads ROI -->
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm border-t-4 border-t-blue-500">
                        <p class="text-sm font-medium text-slate-500 mb-1"><i class="fa-solid fa-ad text-blue-500 mr-1"></i> Paid Ads (CPAS/Search)</p>
                        <h3 id="mechanic-ads-spend" class="text-2xl font-bold text-slate-800">฿180,000 <span class="text-sm text-slate-400 font-normal">Spend</span></h3>
                        <div class="mt-3 bg-slate-50 p-2 rounded flex justify-between items-center text-sm">
                            <span class="text-slate-600">Generated GMV:</span>
                            <span id="mechanic-ads-gmv" class="font-bold text-slate-800">฿720,000</span>
                        </div>
                        <p id="mechanic-ads-roas" class="text-sm font-bold text-blue-600 mt-2">ROAS: 4.0x</p>
                    </div>

                    <!-- Livestream -->
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm border-t-4 border-t-red-500">
                        <p class="text-sm font-medium text-slate-500 mb-1"><i class="fa-solid fa-video text-red-500 mr-1"></i> Livestream (Shopee/TikTok)</p>
                        <h3 id="mechanic-live-views" class="text-2xl font-bold text-slate-800">45,200 <span class="text-sm text-slate-400 font-normal">Viewers</span></h3>
                        <div class="mt-3 bg-slate-50 p-2 rounded flex justify-between items-center text-sm">
                            <span class="text-slate-600">Generated GMV:</span>
                            <span id="mechanic-live-gmv" class="font-bold text-slate-800">฿350,000</span>
                        </div>
                        <p id="mechanic-live-sessions" class="text-sm font-bold text-red-600 mt-2">18 Sessions MTD</p>
                    </div>

                    <!-- Affiliate -->
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm border-t-4 border-t-purple-500">
                        <p class="text-sm font-medium text-slate-500 mb-1"><i class="fa-solid fa-handshake text-purple-500 mr-1"></i> Affiliates & KOLs</p>
                        <h3 id="mechanic-affiliate-creators" class="text-2xl font-bold text-slate-800">124 <span class="text-sm text-slate-400 font-normal">Active Creators</span></h3>
                        <div class="mt-3 bg-slate-50 p-2 rounded flex justify-between items-center text-sm">
                            <span class="text-slate-600">Generated GMV:</span>
                            <span id="mechanic-affiliate-gmv" class="font-bold text-slate-800">฿255,000</span>
                        </div>
                        <p id="mechanic-affiliate-comm" class="text-sm font-bold text-purple-600 mt-2">Avg Commission: 12%</p>
                    </div>

                    <!-- Organic / Other -->
                    <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm border-t-4 border-t-slate-400">
                        <p class="text-sm font-medium text-slate-500 mb-1"><i class="fa-solid fa-leaf text-slate-400 mr-1"></i> Organic/Direct</p>
                        <h3 id="mechanic-organic-uv" class="text-2xl font-bold text-slate-800">110,200 <span class="text-sm text-slate-400 font-normal">UVs</span></h3>
                        <div class="mt-3 bg-slate-50 p-2 rounded flex justify-between items-center text-sm">
                            <span class="text-slate-600">Generated GMV:</span>
                            <span id="mechanic-organic-gmv" class="font-bold text-slate-800">฿100,000</span>
                        </div>
                        <p class="text-sm font-bold text-slate-500 mt-2">Baseline Traffic</p>
                    </div>
                </div>

                <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden mb-8">
                    <div class="px-6 py-4 border-b border-slate-200 bg-slate-50">
                        <h3 class="text-base font-bold text-slate-800">Mechanics Breakdown Summary</h3>
                    </div>
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="text-xs text-slate-500 uppercase tracking-wider border-b border-slate-200">
                                <th class="px-6 py-4 font-semibold">Mechanic / Channel</th>
                                <th class="px-6 py-4 font-semibold text-right">Orders Driven</th>
                                <th class="px-6 py-4 font-semibold text-right">GMV (Sales)</th>
                                <th class="px-6 py-4 font-semibold text-right">Cost/Spend</th>
                                <th class="px-6 py-4 font-semibold text-right">ROI / ROAS</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100">
                            <tr>
                                <td class="px-6 py-4 font-medium"><i class="fa-brands fa-tiktok text-tiktok mr-2"></i>TikTok Live</td>
                                <td class="px-6 py-4 text-right">720</td>
                                <td class="px-6 py-4 text-right">฿210,000</td>
                                <td class="px-6 py-4 text-right text-slate-500">฿25,000 (Host/Boost)</td>
                                <td class="px-6 py-4 text-right font-bold text-green-600">8.4x</td>
                            </tr>
                            <tr>
                                <td class="px-6 py-4 font-medium"><i class="fa-solid fa-bullhorn text-shopee mr-2"></i>Shopee CPAS Ads</td>
                                <td class="px-6 py-4 text-right">1,400</td>
                                <td class="px-6 py-4 text-right">฿420,000</td>
                                <td class="px-6 py-4 text-right text-slate-500">฿100,000</td>
                                <td class="px-6 py-4 text-right font-bold text-blue-600">4.2x</td>
                            </tr>
                            <tr>
                                <td class="px-6 py-4 font-medium"><i class="fa-solid fa-bullhorn text-lazada mr-2"></i>Lazada Sponsored Search</td>
                                <td class="px-6 py-4 text-right">850</td>
                                <td class="px-6 py-4 text-right">฿300,000</td>
                                <td class="px-6 py-4 text-right text-slate-500">฿80,000</td>
                                <td class="px-6 py-4 text-right font-bold text-blue-600">3.75x</td>
                            </tr>
                            <tr>
                                <td class="px-6 py-4 font-medium"><i class="fa-solid fa-users text-purple-500 mr-2"></i>Shopee Affiliate Network</td>
                                <td class="px-6 py-4 text-right">930</td>
                                <td class="px-6 py-4 text-right">฿255,000</td>
                                <td class="px-6 py-4 text-right text-slate-500">฿30,600 (Comm)</td>
                                <td class="px-6 py-4 text-right font-bold text-purple-600">8.3x</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- ========================================== -->
            <!-- PAGE 3: PERFORMANCE DEEP-DIVE              -->
            <!-- ========================================== -->
            <div id="page-deep-dive" class="page-content hidden">
                <div class="mb-6 flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-2xl font-bold text-slate-800">Channel Performance Deep-Dive</h2>
                        <p class="text-slate-500 text-sm mt-1">Granular breakdown of operational mechanics to evaluate brand growth.</p>
                    </div>
                    <div>
                        <button onclick="auditChannelBudgets()" class="bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-700 hover:to-teal-700 text-white font-semibold py-2 px-4 rounded-lg shadow-sm flex items-center gap-2 transition-all">
                            <span>✨ Run AI Budget Audit</span>
                        </button>
                    </div>
                </div>

                <!-- AI Budget Auditor Box -->
                <div id="deepDiveSummaryBox" class="hidden mb-8 bg-gradient-to-r from-slate-50 to-emerald-50 border border-emerald-200 rounded-xl p-6 shadow-sm relative">
                    <button onclick="closeSummaryBox('deepDiveSummaryBox')" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                        <i class="fa-solid fa-xmark text-lg"></i>
                    </button>
                    <div class="flex items-start gap-4">
                        <div class="text-2xl text-emerald-600 mt-1">
                            <i class="fa-solid fa-calculator"></i>
                        </div>
                        <div class="flex-1">
                            <h4 class="font-bold text-slate-900 mb-2">✨ Channel Reallocation Strategy (AI Auditor)</h4>
                            <div id="deepDiveSummaryText" class="text-slate-700 text-sm space-y-2 whitespace-pre-wrap leading-relaxed">
                                Auditing metrics...
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Sub-tab Bar -->
                <div class="flex border-b border-slate-200 mb-6 gap-6">
                    <button onclick="switchDeepDiveTab('ads-sub-tab', this)" class="sub-tab active pb-3 text-sm font-medium border-b-2 border-transparent hover:text-brand transition-colors">
                        <i class="fa-solid fa-ad mr-1"></i> Paid Ads Funnel
                    </button>
                    <button onclick="switchDeepDiveTab('live-sub-tab', this)" class="sub-tab pb-3 text-sm font-medium border-b-2 border-transparent hover:text-brand transition-colors">
                        <i class="fa-solid fa-video mr-1"></i> Livestream Analysis
                    </button>
                    <button onclick="switchDeepDiveTab('affiliate-sub-tab', this)" class="sub-tab pb-3 text-sm font-medium border-b-2 border-transparent hover:text-brand transition-colors">
                        <i class="fa-solid fa-handshake mr-1"></i> Affiliate Network
                    </button>
                </div>

                <!-- Ads Sub-tab Content -->
                <div id="ads-sub-tab" class="deep-dive-panel block space-y-6">
                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                        <!-- Ads Funnel Widget -->
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm col-span-1 flex flex-col justify-between">
                            <h3 class="font-bold text-slate-800 mb-4">Paid Ads Conversion Funnel</h3>
                            <div class="space-y-4">
                                <div>
                                    <div class="flex justify-between text-xs font-semibold text-slate-500 mb-1">
                                        <span>1. Impressions (Paid)</span>
                                        <span id="ads-funnel-imp">2,450,000</span>
                                    </div>
                                    <div class="w-full bg-slate-100 h-3 rounded-full overflow-hidden">
                                        <div class="bg-blue-400 h-full" style="width: 100%"></div>
                                    </div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-xs font-semibold text-slate-500 mb-1">
                                        <span>2. Clicks (Traffic)</span>
                                        <span id="ads-funnel-click">122,500</span>
                                    </div>
                                    <div class="w-full bg-slate-100 h-3 rounded-full overflow-hidden">
                                        <div class="bg-blue-500 h-full" style="width: 5%"></div>
                                    </div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-xs font-semibold text-slate-500 mb-1">
                                        <span>3. Purchases (GMV)</span>
                                        <span id="ads-funnel-conv">3,120</span>
                                    </div>
                                    <div class="w-full bg-slate-100 h-3 rounded-full overflow-hidden">
                                        <div class="bg-blue-600 h-full" style="width: 2.5%"></div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Platform Ads Grid -->
                        <div class="lg:col-span-2 bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                            <div class="px-6 py-4 border-b border-slate-200 bg-slate-50">
                                <h3 class="font-bold text-slate-800">Ads KPI by Marketplace Solution</h3>
                            </div>
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="text-xs text-slate-500 uppercase tracking-wider border-b border-slate-200">
                                        <th class="px-6 py-3 font-semibold">Solution</th>
                                        <th class="px-4 py-3 font-semibold text-right">CTR%</th>
                                        <th class="px-4 py-3 font-semibold text-right">CPC (THB)</th>
                                        <th class="px-4 py-3 font-semibold text-right">CAC/CPA</th>
                                        <th class="px-4 py-3 font-semibold text-right">Spend</th>
                                        <th class="px-4 py-3 font-semibold text-right">ROAS</th>
                                    </tr>
                                </thead>
                                <tbody id="ads-breakdown-rows" class="divide-y divide-slate-100 text-sm">
                                    <!-- Injected dynamically -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- Livestream Sub-tab Content -->
                <div id="live-sub-tab" class="deep-dive-panel hidden space-y-6">
                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                        <!-- Live Core Metrics -->
                        <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm space-y-4">
                            <h3 class="font-bold text-slate-800">Livestream Engagement</h3>
                            <div>
                                <p class="text-xs text-slate-500 mb-1">Peak Concurrent Viewers (PCV)</p>
                                <h4 id="live-pcv" class="text-xl font-bold text-slate-800">4,200 Viewers</h4>
                            </div>
                            <div>
                                <p class="text-xs text-slate-500 mb-1">Avg. View Duration</p>
                                <h4 id="live-duration" class="text-xl font-bold text-slate-800">3.8 mins</h4>
                            </div>
                            <div>
                                <p class="text-xs text-slate-500 mb-1">Basket Add-to-Cart % (CO%)</p>
                                <h4 id="live-cart-rate" class="text-xl font-bold text-slate-800">12.5%</h4>
                            </div>
                        </div>

                        <!-- Live Session Table -->
                        <div class="lg:col-span-2 bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                            <div class="px-6 py-4 border-b border-slate-200 bg-slate-50">
                                <h3 class="font-bold text-slate-800">Top Livestream Broadcast Logs</h3>
                            </div>
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="text-xs text-slate-500 uppercase tracking-wider border-b border-slate-200">
                                        <th class="px-6 py-3 font-semibold">Session Title</th>
                                        <th class="px-4 py-3 font-semibold text-right">Total Views</th>
                                        <th class="px-4 py-3 font-semibold text-right">Product Clicks</th>
                                        <th class="px-4 py-3 font-semibold text-right">Orders</th>
                                        <th class="px-6 py-3 font-semibold text-right">GMV (THB)</th>
                                    </tr>
                                </thead>
                                <tbody id="live-sessions-rows" class="divide-y divide-slate-100 text-sm">
                                    <!-- Injected dynamically -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- Affiliate Sub-tab Content -->
                <div id="affiliate-sub-tab" class="deep-dive-panel hidden space-y-6">
                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                        <!-- Affiliate KOL Tier Distribution -->
                        <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col justify-between">
                            <h3 class="font-bold text-slate-800 mb-4">KOL Tier GMV Share</h3>
                            <div class="space-y-4 flex-1 flex flex-col justify-center">
                                <div>
                                    <div class="flex justify-between text-xs text-slate-500 mb-1">
                                        <span>Mega / Star Influencers (>1M)</span>
                                        <span id="aff-mega-pct" class="font-bold text-slate-800">35%</span>
                                    </div>
                                    <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                                        <div class="bg-purple-600 h-full" style="width: 35%"></div>
                                    </div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-xs text-slate-500 mb-1">
                                        <span>Macro / Mid KOLs (100k - 1M)</span>
                                        <span id="aff-macro-pct" class="font-bold text-slate-800">45%</span>
                                    </div>
                                    <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                                        <div class="bg-indigo-600 h-full" style="width: 45%"></div>
                                    </div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-xs text-slate-500 mb-1">
                                        <span>Micro / Nano Creators (<100k)</span>
                                        <span id="aff-micro-pct" class="font-bold text-slate-800">20%</span>
                                    </div>
                                    <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                                        <div class="bg-blue-600 h-full" style="width: 20%"></div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Top Affiliates Board -->
                        <div class="lg:col-span-2 bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                            <div class="px-6 py-4 border-b border-slate-200 bg-slate-50">
                                <h3 class="font-bold text-slate-800">Affiliate Leaderboard (TH)</h3>
                            </div>
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="text-xs text-slate-500 uppercase tracking-wider border-b border-slate-200">
                                        <th class="px-6 py-3 font-semibold">Creator ID</th>
                                        <th class="px-4 py-3 font-semibold text-center">Platform</th>
                                        <th class="px-4 py-3 font-semibold text-right">Items Sold</th>
                                        <th class="px-4 py-3 font-semibold text-right">Commission Tier</th>
                                        <th class="px-6 py-3 font-semibold text-right">GMV Contribution</th>
                                    </tr>
                                </thead>
                                <tbody id="affiliate-leader-rows" class="divide-y divide-slate-100 text-sm">
                                    <!-- Injected dynamically -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- ========================================== -->
            <!-- PAGE 4: PRODUCT & CATEGORY                 -->
            <!-- ========================================== -->
            <div id="page-products" class="page-content hidden">
                <div class="mb-6 flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-2xl font-bold text-slate-800">Category & Product Movement</h2>
                        <p class="text-slate-500 text-sm mt-1">Identify top-moving categories and monitor SKU-level inventory health.</p>
                    </div>
                    <div>
                        <button onclick="generateInventoryPlan()" class="bg-gradient-to-r from-amber-600 to-orange-600 hover:from-amber-700 hover:to-orange-700 text-white font-semibold py-2 px-4 rounded-lg shadow-sm flex items-center gap-2 transition-all">
                            <span>✨ Create Stock-out Mitigation Strategy</span>
                        </button>
                    </div>
                </div>

                <!-- Product Inventory Plan Panel -->
                <div id="productsSummaryBox" class="hidden mb-8 bg-gradient-to-r from-slate-50 to-amber-50 border border-amber-200 rounded-xl p-6 shadow-sm relative">
                    <button onclick="closeSummaryBox('productsSummaryBox')" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                        <i class="fa-solid fa-xmark text-lg"></i>
                    </button>
                    <div class="flex items-start gap-4">
                        <div class="text-2xl text-amber-600 mt-1">
                            <i class="fa-solid fa-boxes-packing"></i>
                        </div>
                        <div class="flex-1">
                            <h4 class="font-bold text-slate-900 mb-2 flex items-center gap-2">
                                ✨ SKU Inventory & SLA Safeguard (AI Pilot)
                            </h4>
                            <div id="productsSummaryText" class="text-slate-700 text-sm space-y-2 whitespace-pre-wrap leading-relaxed">
                                Loading analysis...
                            </div>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
                    <!-- Category Mix Chart -->
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col">
                        <h3 class="text-base font-bold text-slate-800 mb-4">GMV by Category</h3>
                        <div class="relative h-64 w-full flex-1">
                            <canvas id="categoryChart"></canvas>
                        </div>
                    </div>

                    <!-- Top SKUs Table -->
                    <div class="lg:col-span-2 bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                        <div class="px-6 py-4 border-b border-slate-200 bg-slate-50 flex justify-between items-center">
                            <h3 class="text-base font-bold text-slate-800">Top Moving SKUs</h3>
                            <button class="text-sm text-brand font-medium">View All</button>
                        </div>
                        <div class="overflow-x-auto h-72">
                            <table class="w-full text-left border-collapse">
                                <thead class="sticky top-0 bg-white">
                                    <tr class="text-xs text-slate-500 uppercase tracking-wider border-b border-slate-200">
                                        <th class="px-6 py-3 font-semibold">SKU / Product Name</th>
                                        <th class="px-4 py-3 font-semibold text-right">Units Sold</th>
                                        <th class="px-4 py-3 font-semibold text-right">GMV</th>
                                        <th class="px-6 py-3 font-semibold text-center">Inventory Health</th>
                                    </tr>
                                </thead>
                                <tbody id="top-skus-body" class="divide-y divide-slate-100 text-sm">
                                    <!-- Dynamic rows injected by JavaScript depending on selected brand -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Footer -->
            <footer class="text-center text-sm text-slate-500 pb-8 mt-4">
                &copy; 2026 OmniEnable Operations Dashboard. All rights reserved.
            </footer>
        </div>
    </main>

    <!-- UI, Mock Data & Gemini Chart Logic -->
    <script>
        const apiKey = ""; // The environment provides the API key at runtime. Do not add static key validation logic.

        // Global dataset supporting cosmetics & tech options, including the new Deep-dive page metrics
        const dataStore = {
            cosmetics: {
                gmv: "฿1,425,000", gmvTarget: "฿1,500,000", gmvPct: "95%",
                orders: "5,140", ordersTarget: "6,000", ordersPct: "85%",
                aov: "฿277", aovTarget: "฿250", aovPct: "110%",
                cr: "2.77%", crTarget: "3.00%", crPct: "92%",
                // Daily Run-Rate metrics
                achievementPct: "95.0%",
                gapTarget: "฿75,000",
                dailyVelocityRequired: "฿25,000 / Day",
                // YoY Comparison Historical Metrics
                yoyPrevSales: 1150000, // May 2025 actual
                yoyCurrSales: 1425000, // May 2026 actual
                yoyTargetSales: 1380000, // May 2026 target (for YoY +20%)
                // Mechanics
                adsSpend: "฿180,000", adsGmv: "฿720,000", adsRoas: "ROAS: 4.0x",
                liveViews: "45,200", liveGmv: "฿350,000", liveSessions: "18 Sessions MTD",
                affCreators: "124", affGmv: "฿255,000", affComm: "Avg Commission: 12%",
                organicUv: "110,200", organicGmv: "฿100,000",
                // Products
                categoryData: [55, 25, 15, 5],
                categoryLabels: ['Skincare', 'Makeup', 'Body Care', 'Accessories'],
                skus: [
                    { name: "Radiant Glow Serum 30ml", units: "1,240", gmv: "฿434,000", health: "Good (>30 days)", healthColor: "green" },
                    { name: "Matte Liquid Lipstick - Ruby", units: "980", gmv: "฿147,000", health: "OOS Risk (5 days)", healthColor: "red" },
                    { name: "Hydrating Night Cream 50g", units: "850", gmv: "฿212,500", health: "Good (22 days)", healthColor: "green" },
                    { name: "UV Shield Sunscreen SPF50", units: "720", gmv: "฿180,000", health: "Low (12 days)", healthColor: "yellow" }
                ],
                // Page 3: Deep Dive Channels
                deepDive: {
                    ads: {
                        impressions: "2,450,000", clicks: "122,500", conversions: "3,120",
                        solutions: [
                            { name: "Shopee CPAS Ads", ctr: "5.1%", cpc: "฿1.8", cpa: "฿71", spend: "฿100,000", roas: "4.2x" },
                            { name: "Lazada Sponsored Search", ctr: "4.2%", cpc: "฿2.2", cpa: "฿94", spend: "฿50,000", roas: "3.7x" },
                            { name: "TikTok Video Shopping Ads", ctr: "5.8%", cpc: "฿1.4", cpa: "฿64", spend: "฿30,000", roas: "4.8x" }
                        ]
                    },
                    live: {
                        pcv: "4,200 Viewers", duration: "3.8 mins", coRate: "12.5%",
                        sessions: [
                            { title: "TikTok 5.5 Mega Sale Rush", views: "18,400", clicks: "4,600", orders: "552", gmv: "฿165,600" },
                            { title: "Shopee Live: Mid-Month Beauty", views: "14,100", clicks: "3,100", orders: "341", gmv: "฿102,300" },
                            { title: "Lazada Live Everyday Skincare", views: "12,700", clicks: "2,200", orders: "220", gmv: "฿66,000" }
                        ]
                    },
                    affiliate: {
                        mega: "35%", macro: "45%", micro: "20%",
                        creators: [
                            { id: "@pimrypie_official", platform: "TikTok", units: "640", comm: "15%", gmv: "฿192,000" },
                            { id: "@icepadie_makeup", platform: "TikTok", views: "210", comm: "10%", gmv: "฿42,000" },
                            { id: "@beauty_blogger_th", platform: "Shopee Network", units: "80", comm: "12%", gmv: "฿21,000" }
                        ]
                    }
                },
                // Discrete full month daily actuals & daily targets
                dailyActuals: [38, 41, 39, 42, 68, 55, 40, 39, 44, 43, 41, 46, 52, 61, 48, 42, 38, 40, 42, 45, 49, 58, 51, 44, 43, 41, 45, 48, null, null, null], // Null for remaining 3 days
                dailyTargets: [40, 40, 40, 40, 60, 45, 42, 42, 42, 42, 42, 42, 42, 55, 45, 42, 42, 42, 42, 42, 42, 50, 45, 42, 42, 42, 42, 42, 42, 42, 42]
            },
            tech: {
                gmv: "฿3,240,000", gmvTarget: "฿3,000,000", gmvPct: "108%",
                orders: "2,150", ordersTarget: "2,000", ordersPct: "107%",
                aov: "฿1,506", aovTarget: "฿1,500", aovPct: "100.4%",
                cr: "1.85%", crTarget: "1.80%", crPct: "102%",
                // Daily Run-Rate metrics
                achievementPct: "108.0%",
                gapTarget: "-฿240,000 (Met)",
                dailyVelocityRequired: "฿0 / Day (Goal Hit)",
                // YoY Comparison Historical Metrics
                yoyPrevSales: 2500000, // May 2025 actual
                yoyCurrSales: 3240000, // May 2026 actual
                yoyTargetSales: 3000000, // May 2026 target
                // Mechanics
                adsSpend: "฿410,000", adsGmv: "฿1,850,000", adsRoas: "ROAS: 4.5x",
                liveViews: "21,300", liveGmv: "฿580,000", liveSessions: "8 Sessions MTD",
                affCreators: "85", affGmv: "฿460,000", affComm: "Avg Commission: 15%",
                organicUv: "94,000", organicGmv: "฿350,000",
                // Products
                categoryData: [45, 30, 20, 5],
                categoryLabels: ['Mobile Accs', 'Smart Home', 'Wearables', 'Audio'],
                skus: [
                    { name: "Apex Pro Wireless ANC Headset", units: "620", gmv: "฿930,000", health: "Good (>45 days)", healthColor: "green" },
                    { name: "Smart Plug PowerGrip V2", units: "950", gmv: "฿570,000", health: "OOS Risk (3 days)", healthColor: "red" },
                    { name: "Titanium FitBand Active", units: "410", gmv: "฿1,025,000", health: "Good (18 days)", healthColor: "green" },
                    { name: "Qi2 Magnetic Charging Dock", units: "170", gmv: "฿715,000", health: "Low (9 days)", healthColor: "yellow" }
                ],
                // Page 3: Deep Dive Channels
                deepDive: {
                    ads: {
                        impressions: "4,500,000", clicks: "185,000", conversions: "2,450",
                        solutions: [
                            { name: "Shopee CPAS Ads", ctr: "3.8%", cpc: "฿4.5", cpa: "฿280", spend: "฿250,000", roas: "4.8x" },
                            { name: "Lazada Sponsored Search", ctr: "3.1%", cpc: "฿5.2", cpa: "฿310", spend: "฿110,000", roas: "4.1x" },
                            { name: "TikTok Video Shopping Ads", ctr: "4.5%", cpc: "฿3.8", cpa: "฿240", spend: "฿50,000", roas: "4.6x" }
                        ]
                    },
                    live: {
                        pcv: "1,800 Viewers", duration: "5.4 mins", coRate: "8.2%",
                        sessions: [
                            { title: "Smart Home Tech Talk: Live V2", views: "10,200", clicks: "1,500", orders: "123", gmv: "฿369,000" },
                            { title: "Apex Sound Premium Launch", views: "6,400", clicks: "1,100", orders: "85", gmv: "฿170,000" },
                            { title: "TikTok Tech Gadgets Roundup", views: "4,700", clicks: "510", orders: "21", gmv: "฿41,000" }
                        ]
                    },
                    affiliate: {
                        mega: "20%", macro: "50%", micro: "30%",
                        creators: [
                            { id: "@tech_unboxer_th", platform: "TikTok", units: "110", comm: "15%", gmv: "฿275,000" },
                            { id: "@gadget_lover_bkk", platform: "Lazada Partner", views: "50", comm: "12%", gmv: "฿125,000" },
                            { id: "@ios_android_geek", platform: "Shopee Network", units: "30", comm: "15%", gmv: "฿60,000" }
                        ]
                    }
                },
                // Discrete full month daily actuals & daily targets
                dailyActuals: [88, 92, 91, 105, 140, 115, 96, 94, 98, 95, 96, 99, 112, 138, 118, 102, 94, 95, 98, 104, 106, 128, 115, 102, 98, 95, 102, 109, null, null, null],
                dailyTargets: [90, 90, 90, 90, 120, 100, 95, 95, 95, 95, 95, 95, 95, 120, 100, 95, 95, 95, 95, 95, 95, 110, 100, 95, 95, 95, 95, 95, 95, 95, 95]
            }
        };

        // UI chart instance variables
        let yoyGrowthChartInst = null;
        let dailyVelocityChartInst = null;
        let platformShareChartInst = null;
        let categoryChartInst = null;

        // Exponential Backoff API Wrapper for Gemini API
        async function callGemini(systemPrompt, userPrompt) {
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            const payload = {
                contents: [{ parts: [{ text: userPrompt }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] }
            };

            let delay = 1000;
            for (let i = 0; i < 5; i++) {
                try {
                    const response = await fetch(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error(`HTTP Error Status: ${response.status}`);
                    const result = await response.json();
                    return result.candidates?.[0]?.content?.parts?.[0]?.text || "No response received from model.";
                } catch (error) {
                    if (i === 4) {
                        console.error("Gemini API calling failed after 5 attempts:", error);
                        return "Oops! We encountered an error preparing your AI analysis. Please verify your connection and try again.";
                    }
                    await new Promise(resolve => setTimeout(resolve, delay));
                    delay *= 2; // Exponential Backoff
                }
            }
        }

        // Close Summary Panels
        function closeSummaryBox(boxId) {
            const box = document.getElementById(boxId);
            if (box) box.classList.add('hidden');
        }

        // Feature 1: Executive Overview Report Generator (Page 1)
        async function generateOverviewSummary() {
            const selector = document.getElementById('brandSelector');
            if (!selector) return;
            const currentBrand = selector.value;
            const data = dataStore[currentBrand];
            const summaryBox = document.getElementById('overviewSummaryBox');
            const summaryText = document.getElementById('overviewSummaryText');

            if (summaryBox) summaryBox.classList.remove('hidden');
            if (summaryText) summaryText.innerHTML = `<div class="flex items-center gap-2"><i class="fa-solid fa-circle-notch animate-spin text-blue-600"></i> Thinking, compiling platform data and pacing scores...</div>`;

            const systemPrompt = `You are a world-class senior e-commerce enabler operating specifically in the Thailand market. 
Your target audience is the brand director. Present a super-concise executive summary (under 250 words) outlining the current monthly pacing against targets, highlighting strong and weak aspects of platform participation (Shopee, Lazada, TikTok Shop). 
Use professional corporate tone, write in clear English, mention Thai local double-day shopping trends if relevant (e.g., May 25th Mid-Month or upcoming 6.6 campaign preparations). Do not use fancy markdown templates, but do use standard bullet points for readability.`;

            const userPrompt = `Generate a performance summary based on this exact operational data:
- Brand Name: ${currentBrand === 'cosmetics' ? 'Acme Cosmetics TH' : 'TechGear Plus'}
- GMV Achieved: ${data.gmv} (Target: ${data.gmvTarget}, Pacing: ${data.gmvPct})
- Orders Completed: ${data.orders} (Target: ${data.ordersTarget}, Pacing: ${data.ordersPct})
- AOV: ${data.aov}
- CR% (Blended): ${data.cr} (Target: ${data.crTarget})`;

            const response = await callGemini(systemPrompt, userPrompt);
            if (summaryText) summaryText.innerHTML = response.replace(/\n/g, "<br>");
        }

        // Feature 2: Growth Campaign Mechanic Optimizer MTD (Page 2)
        async function generateMechanicsOptimization() {
            const selector = document.getElementById('brandSelector');
            if (!selector) return;
            const currentBrand = selector.value;
            const data = dataStore[currentBrand];
            const summaryBox = document.getElementById('mechanicsSummaryBox');
            const summaryText = document.getElementById('mechanicsSummaryText');

            if (summaryBox) summaryBox.classList.remove('hidden');
            if (summaryText) summaryText.innerHTML = `<div class="flex items-center gap-2"><i class="fa-solid fa-circle-notch animate-spin text-violet-600"></i> Running performance diagnostics on Ads, Live broadcasts, and Affiliate networks...</div>`;

            const systemPrompt = `You are a Growth Marketer & Channel Optimizer specializing in Thai marketplaces (Lazada, Shopee, TikTok Shop TH). 
Analyze the brand's metrics on Paid Spends, Livestreams, and Affiliate drivers. Recommend exactly 3 actionable, hyper-localized tactical improvements for immediate implementation (such as optimizing Shopee CPAS, scaling TikTok Live sessions, or adapting affiliate commission tiers for local Thai creators). Keep it tactical, strategic, and direct.`;

            const userPrompt = `Develop a marketing optimization framework based on these marketing channel inputs:
- Paid Ads Spends: ${data.adsSpend} driving ${data.adsGmv} (${data.adsRoas})
- Live Broadcasts: ${data.liveViews} views, generating ${data.liveGmv} (${data.liveSessions})
- Creator Affiliate Spends: ${data.affCreators} creators generating ${data.affGmv} (Avg Commission: ${data.affComm})
- Organic baseline GMV: ${data.organicGmv} with ${data.organicUv} UVs.`;

            const response = await callGemini(systemPrompt, userPrompt);
            if (summaryText) summaryText.innerHTML = response.replace(/\n/g, "<br>");
        }

        // Feature 3: Deep-Dive Budget Audit Assistant (Page 3)
        async function auditChannelBudgets() {
            const selector = document.getElementById('brandSelector');
            if (!selector) return;
            const currentBrand = selector.value;
            const data = dataStore[currentBrand];
            const summaryBox = document.getElementById('deepDiveSummaryBox');
            const summaryText = document.getElementById('deepDiveSummaryText');

            if (summaryBox) summaryBox.classList.remove('hidden');
            if (summaryText) summaryText.innerHTML = `<div class="flex items-center gap-2"><i class="fa-solid fa-circle-notch animate-spin text-emerald-600"></i> Conducting micro-funnel analysis on platform ad CTRs, live metrics and affiliates...</div>`;

            const systemPrompt = `You are a Senior E-Commerce Media Planner. Review the detailed channel metrics and suggest a smart budget reallocation strategy.
Point out which marketplace ad engine or live session is the clear winner and suggest exactly how much budget to shift (e.g. "We suggest transferring 20% of Lazada sponsored search spend into TikTok Live"). Highlight CPC/CPA differences and influencer tier efficiency. No markdown wrappers, present as neat corporate bullets.`;

            const adsList = data.deepDive.ads.solutions.map(s => `${s.name}: CTR=${s.ctr}, CPC=${s.cpc}, Spend=${s.spend}, ROAS=${s.roas}`).join(" | ");
            const liveList = data.deepDive.live.sessions.map(s => `${s.title}: Views=${s.views}, Orders=${s.orders}, GMV=${s.gmv}`).join(" | ");
            const affiliateList = `KOL Split: Mega=${data.deepDive.affiliate.mega}, Macro=${data.deepDive.affiliate.macro}, Micro/Nano=${data.deepDive.affiliate.micro}.`;

            const userPrompt = `Analyze and provide a budget audit for this specific data:
- Brand: ${currentBrand === 'cosmetics' ? 'Acme Cosmetics' : 'TechGear'}
- Ads Channels: ${adsList}
- Live Broadcast Performance: ${liveList}
- Affiliate distribution: ${affiliateList}`;

            const response = await callGemini(systemPrompt, userPrompt);
            if (summaryText) summaryText.innerHTML = response.replace(/\n/g, "<br>");
        }

        // Feature 4: Urgent Inventory & Logistics SLA Safeguard Planner (Page 4)
        async function generateInventoryPlan() {
            const selector = document.getElementById('brandSelector');
            if (!selector) return;
            const currentBrand = selector.value;
            const data = dataStore[currentBrand];
            const summaryBox = document.getElementById('productsSummaryBox');
            const summaryText = document.getElementById('productsSummaryText');

            if (summaryBox) summaryBox.classList.remove('hidden');
            if (summaryText) summaryText.innerHTML = `<div class="flex items-center gap-2"><i class="fa-solid fa-circle-notch animate-spin text-amber-600"></i> Calculating stock velocity and platform SLA penalty risks...</div>`;

            const highRiskSku = data.skus.find(sku => sku.healthColor === 'red');

            const systemPrompt = `You are an E-Commerce supply chain manager and platform health champion. 
We have a critical stock-out risk for our top SKU that will hurt store algorithm ranking if not addressed immediately. 
Provide:
1) A 1-sentence assessment of the algorithmic penalty danger on Shopee/Lazada (e.g. non-fulfillment penalty points).
2) A professional urgent restock draft email to send to the manufacturing supplier (written in professional English).
3) A 2-bullet tactical playbook (such as launching pre-order listings or shifting live traffic to healthy alternate SKUs) to mitigate sales disruption.`;

            const userPrompt = `Create an inventory safeguard playbook based on this scenario:
- Top Risk SKU: "${highRiskSku.name}"
- Remaining supply runway: Only ${highRiskSku.health} left!
- Units Sold: ${highRiskSku.units} units sold MTD, generating ${highRiskSku.gmv}.`;

            const response = await callGemini(systemPrompt, userPrompt);
            if (summaryText) summaryText.innerHTML = response.replace(/\n/g, "<br>");
        }

        // Page Switcher
        function switchPage(pageId, navElement) {
            document.querySelectorAll('.page-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.page-content').forEach(el => el.classList.remove('block'));
            
            const targetPage = document.getElementById(pageId);
            if (targetPage) {
                targetPage.classList.remove('hidden');
                targetPage.classList.add('block');
            }

            document.querySelectorAll('.nav-link').forEach(el => {
                el.classList.remove('active', 'bg-brand', 'text-white');
                el.classList.add('text-slate-300');
            });
            navElement.classList.add('active', 'bg-brand', 'text-white');
            navElement.classList.remove('text-slate-300', 'hover:bg-slate-800');
            
            window.dispatchEvent(new Event('resize'));
        }

        // Sub-Tab Switcher for Channel Deep-Dive
        function switchDeepDiveTab(panelId, element) {
            document.querySelectorAll('.deep-dive-panel').forEach(panel => panel.classList.add('hidden'));
            document.querySelectorAll('.deep-dive-panel').forEach(panel => panel.classList.remove('block'));

            const targetPanel = document.getElementById(panelId);
            if (targetPanel) {
                targetPanel.classList.remove('hidden');
                targetPanel.classList.add('block');
            }

            document.querySelectorAll('.sub-tab').forEach(tab => tab.classList.remove('active'));
            element.classList.add('active');
        }

        // Update brand specific datasets dynamically with element checks
        function updateBrandData() {
            const selector = document.getElementById('brandSelector');
            if (!selector) return;
            const brand = selector.value;
            const data = dataStore[brand];
            if (!data) return;

            // Helper function to safely set element properties
            const setSafeText = (id, text) => {
                const el = document.getElementById(id);
                if (el) el.innerText = text;
            };
            const setSafeWidth = (id, width) => {
                const el = document.getElementById(id);
                if (el) el.style.width = width;
            };
            const setSafeHTML = (id, html) => {
                const el = document.getElementById(id);
                if (el) el.innerHTML = html;
            };

            // Update main metrics (Page 1)
            setSafeText('overview-gmv', data.gmv);
            setSafeText('overview-gmv-target', "Target: " + data.gmvTarget);
            setSafeText('overview-gmv-pct', data.gmvPct);
            setSafeWidth('overview-gmv-bar', data.gmvPct);

            setSafeText('overview-orders', data.orders);
            setSafeText('overview-orders-target', "Target: " + data.ordersTarget);
            setSafeText('overview-orders-pct', data.ordersPct);
            setSafeWidth('overview-orders-bar', data.ordersPct);

            setSafeText('overview-aov', data.aov);
            setSafeText('overview-aov-target', "Target: " + data.aovTarget);
            setSafeText('overview-aov-pct', data.aovPct);
            setSafeWidth('overview-aov-bar', parseInt(data.aovPct) > 100 ? "100%" : data.aovPct);

            setSafeText('overview-cr', data.cr);
            setSafeText('overview-cr-target', "Target: " + data.crTarget);
            setSafeText('overview-cr-pct', data.crPct);
            setSafeWidth('overview-cr-bar', data.crPct);

            // Update Daily Run-Rate scorecards
            setSafeText('runrate-pct-score', data.achievementPct);
            setSafeText('runrate-rem-score', data.gapTarget);
            setSafeText('runrate-daily-req', data.dailyVelocityRequired);

            // Page 2 metrics
            setSafeHTML('mechanic-ads-spend', `${data.adsSpend} <span class="text-sm text-slate-400 font-normal">Spend</span>`);
            setSafeText('mechanic-ads-gmv', data.adsGmv);
            setSafeText('mechanic-ads-roas', data.adsRoas);

            setSafeHTML('mechanic-live-views', `${data.liveViews} <span class="text-sm text-slate-400 font-normal">Viewers</span>`);
            setSafeText('mechanic-live-gmv', data.liveGmv);
            setSafeText('mechanic-live-sessions', data.liveSessions);

            setSafeHTML('mechanic-affiliate-creators', `${data.affCreators} <span class="text-sm text-slate-400 font-normal">Active Creators</span>`);
            setSafeText('mechanic-affiliate-gmv', data.affGmv);
            setSafeText('mechanic-affiliate-comm', data.affComm);

            setSafeHTML('mechanic-organic-uv', `${data.organicUv} <span class="text-sm text-slate-400 font-normal">UVs</span>`);
            setSafeText('mechanic-organic-gmv', data.organicGmv);

            // Page 3: Channel Deep-Dive Metrics
            setSafeText('ads-funnel-imp', data.deepDive.ads.impressions);
            setSafeText('ads-funnel-click', data.deepDive.ads.clicks);
            setSafeText('ads-funnel-conv', data.deepDive.ads.conversions);

            // Inject Ads KPI Rows
            const adsRows = document.getElementById('ads-breakdown-rows');
            if (adsRows) {
                adsRows.innerHTML = '';
                data.deepDive.ads.solutions.forEach(s => {
                    adsRows.innerHTML += `
                        <tr class="hover:bg-slate-50 transition-colors">
                            <td class="px-6 py-4 font-medium text-slate-800">${s.name}</td>
                            <td class="px-4 py-4 text-right">${s.ctr}</td>
                            <td class="px-4 py-4 text-right">${s.cpc}</td>
                            <td class="px-4 py-4 text-right">${s.cpa}</td>
                            <td class="px-4 py-4 text-right text-slate-600">${s.spend}</td>
                            <td class="px-4 py-4 text-right font-bold text-brand">${s.roas}</td>
                        </tr>
                    `;
                });
            }

            // Live metrics
            setSafeText('live-pcv', data.deepDive.live.pcv);
            setSafeText('live-duration', data.deepDive.live.duration);
            setSafeText('live-cart-rate', data.deepDive.live.coRate);

            // Inject Live Sessions Logs
            const liveRows = document.getElementById('live-sessions-rows');
            if (liveRows) {
                liveRows.innerHTML = '';
                data.deepDive.live.sessions.forEach(s => {
                    liveRows.innerHTML += `
                        <tr class="hover:bg-slate-50 transition-colors">
                            <td class="px-6 py-4 font-medium text-slate-800">${s.title}</td>
                            <td class="px-4 py-4 text-right">${s.views}</td>
                            <td class="px-4 py-4 text-right">${s.clicks}</td>
                            <td class="px-4 py-4 text-right">${s.orders}</td>
                            <td class="px-6 py-4 text-right font-bold text-brand">${s.gmv}</td>
                        </tr>
                    `;
                });
            }

            // Affiliate Metrics
            setSafeText('aff-mega-pct', data.deepDive.affiliate.mega);
            setSafeText('aff-macro-pct', data.deepDive.affiliate.macro);
            setSafeText('aff-micro-pct', data.deepDive.affiliate.micro);

            // Inject Affiliates Leaderboard
            const affRows = document.getElementById('affiliate-leader-rows');
            if (affRows) {
                affRows.innerHTML = '';
                data.deepDive.affiliate.creators.forEach(c => {
                    let badgeClass = "bg-slate-100 text-slate-800";
                    if (c.platform.includes("TikTok")) badgeClass = "bg-rose-100 text-rose-700 font-semibold";
                    if (c.platform.includes("Lazada")) badgeClass = "bg-blue-100 text-blue-800 font-semibold";
                    if (c.platform.includes("Shopee")) badgeClass = "bg-orange-100 text-orange-700 font-semibold";

                    affRows.innerHTML += `
                        <tr class="hover:bg-slate-50 transition-colors">
                            <td class="px-6 py-4 font-medium text-slate-800">${c.id}</td>
                            <td class="px-4 py-4 text-center"><span class="px-2 py-1 rounded text-xs ${badgeClass}">${c.platform}</span></td>
                            <td class="px-4 py-4 text-right">${c.units || c.views || '-'}</td>
                            <td class="px-4 py-4 text-right text-slate-600">${c.comm}</td>
                            <td class="px-6 py-4 text-right font-bold text-brand">${c.gmv}</td>
                        </tr>
                    `;
                });
            }

            // Hide summary boxes when brand switches to avoid obsolete AI summaries
            closeSummaryBox('overviewSummaryBox');
            closeSummaryBox('mechanicsSummaryBox');
            closeSummaryBox('deepDiveSummaryBox');
            closeSummaryBox('productsSummaryBox');

            // Page 4: Product Lists rendering
            const skuTableBody = document.getElementById('top-skus-body');
            if (skuTableBody) {
                skuTableBody.innerHTML = '';
                data.skus.forEach(sku => {
                    let badgeClass = "bg-green-100 text-green-700";
                    if(sku.healthColor === "red") badgeClass = "bg-red-100 text-red-700 animate-pulse";
                    if(sku.healthColor === "yellow") badgeClass = "bg-yellow-100 text-yellow-700";

                    skuTableBody.innerHTML += `
                        <tr class="hover:bg-slate-50 transition-colors">
                            <td class="px-6 py-3 font-medium">${sku.name}</td>
                            <td class="px-4 py-3 text-right">${sku.units}</td>
                            <td class="px-4 py-3 text-right">${sku.gmv}</td>
                            <td class="px-6 py-3 text-center"><span class="px-2 py-1 rounded text-xs font-bold ${badgeClass}">${sku.health}</span></td>
                        </tr>
                    `;
                });
            }

            // Update charts with brand contextual configurations
            if (categoryChartInst) {
                categoryChartInst.data.labels = data.categoryLabels;
                categoryChartInst.data.datasets[0].data = data.categoryData;
                categoryChartInst.update();
            }

            // Update YoY Growth Chart
            if (yoyGrowthChartInst) {
                yoyGrowthChartInst.data.datasets[0].data = [data.yoyPrevSales, data.yoyCurrSales];
                yoyGrowthChartInst.data.datasets[1].data = [data.yoyPrevSales, data.yoyTargetSales];
                yoyGrowthChartInst.update();
            }

            // Update Daily Actual vs Target Chart (Discrete)
            if (dailyVelocityChartInst) {
                dailyVelocityChartInst.data.datasets[0].data = data.dailyActuals;
                dailyVelocityChartInst.data.datasets[1].data = data.dailyTargets;
                dailyVelocityChartInst.update();
            }
        }

        document.addEventListener('DOMContentLoaded', function() {
            Chart.defaults.font.family = "'Inter', sans-serif";
            Chart.defaults.color = '#64748b';

            const daysArray = Array.from({length: 31}, (_, i) => `Day ${i+1}`);

            // Initialize YoY Growth Comparison Chart
            const ctxYoY = document.getElementById('yoyGrowthChart');
            if (ctxYoY) {
                yoyGrowthChartInst = new Chart(ctxYoY.getContext('2d'), {
                    type: 'bar',
                    data: {
                        labels: ['May 2025 Actual', 'May 2026 Actual'],
                        datasets: [
                            {
                                label: 'Actual GMV (THB)',
                                data: [1150000, 1425000],
                                backgroundColor: ['#94a3b8', '#3b82f6'],
                                borderRadius: 6,
                                maxBarThickness: 50
                            },
                            {
                                label: 'Target Model (YoY +20%)',
                                data: [1150000, 1380000],
                                backgroundColor: ['transparent', '#10b981'],
                                borderColor: '#10b981',
                                borderWidth: 2,
                                borderDash: [4, 4],
                                type: 'bar',
                                maxBarThickness: 50
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { position: 'bottom' },
                            tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        return context.dataset.label + ': ฿' + context.raw.toLocaleString();
                                    }
                                }
                            }
                        },
                        scales: {
                            y: {
                                beginAtZero: true,
                                grid: { borderDash: [4, 4] },
                                ticks: { callback: value => '฿' + (value / 1000).toLocaleString() + 'k' }
                            },
                            x: { grid: { display: false } }
                        }
                    }
                });
            }

            // Initialize Daily Velocity (Actual vs Target) Non-cumulative Chart
            const ctxDailyVelocity = document.getElementById('dailyVelocityChart');
            if (ctxDailyVelocity) {
                dailyVelocityChartInst = new Chart(ctxDailyVelocity.getContext('2d'), {
                    type: 'bar',
                    data: {
                        labels: daysArray,
                        datasets: [
                            {
                                label: 'Daily Actual GMV (THB)',
                                data: dataStore.cosmetics.dailyActuals,
                                backgroundColor: '#3b82f6',
                                borderRadius: 4
                            },
                            {
                                label: 'Daily Target GMV (THB)',
                                data: dataStore.cosmetics.dailyTargets,
                                type: 'line',
                                borderColor: '#e11d48',
                                borderWidth: 2.5,
                                borderDash: [2, 2],
                                fill: false,
                                pointRadius: 0
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { position: 'bottom' },
                            tooltip: {
                                mode: 'index',
                                intersect: false,
                                callbacks: {
                                    label: function(context) {
                                        if (context.raw === null) return context.dataset.label + ': Pending';
                                        return context.dataset.label + ': ฿' + (context.raw * 1000).toLocaleString();
                                    }
                                }
                            }
                        },
                        scales: {
                            y: {
                                beginAtZero: true,
                                grid: { borderDash: [4, 4] },
                                ticks: { callback: value => '฿' + value.toLocaleString() + 'k' }
                            },
                            x: { grid: { display: false } }
                        }
                    }
                });
            }

            // Initialize Platform Share Doughnut (Overview Page)
            const ctxShare = document.getElementById('platformShareChart');
            if (ctxShare) {
                platformShareChartInst = new Chart(ctxShare.getContext('2d'), {
                    type: 'doughnut',
                    data: {
                        labels: ['Shopee', 'Lazada', 'TikTok Shop'],
                        datasets: [{
                            data: [42, 35, 23],
                            backgroundColor: ['#ee4d2d', '#0f146d', '#000000'],
                            borderWidth: 0, hoverOffset: 4
                        }]
                    },
                    options: {
                        responsive: true, maintainAspectRatio: false, cutout: '70%',
                        plugins: { legend: { position: 'bottom' } }
                    }
                });
            }

            // Initialize Category GMV Chart (Product Page)
            const ctxCat = document.getElementById('categoryChart');
            if (ctxCat) {
                categoryChartInst = new Chart(ctxCat.getContext('2d'), {
                    type: 'bar',
                    data: {
                        labels: ['Skincare', 'Makeup', 'Body Care', 'Accessories'],
                        datasets: [{
                            label: 'GMV Share (%)',
                            data: [55, 25, 15, 5],
                            backgroundColor: ['#3b82f6', '#ec4899', '#8b5cf6', '#94a3b8'],
                            borderRadius: 4
                        }]
                    },
                    options: {
                        indexAxis: 'y', // Horizontal bar chart
                        responsive: true, maintainAspectRatio: false,
                        plugins: { legend: { display: false } },
                        scales: { x: { display: false }, y: { grid: { display: false } } }
                    }
                });
            }

            // Populate all data fields correctly on run
            updateBrandData();
        });
    </script>
</body>
</html>
