<!DOCTYPE html>
<html lang="en" class="scroll-smooth">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>1AItoro - AI-Powered Marketing, Finance & Crypto Insights</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/phosphor-icons"></script>
    <!-- Stripe.js v3 -->
    <script src="https://js.stripe.com/v3/"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0F172A;
            color: #E2E8F0;
        }

        .glass-effect {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px); /* For Safari */
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .gradient-text {
            background: linear-gradient(90deg, #38BDF8, #A78BFA);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .cta-button {
            background-image: linear-gradient(to right, #38BDF8 0%, #818CF8 51%, #A78BFA 100%);
            transition: 0.5s;
            background-size: 200% auto;
        }
        .cta-button:hover {
            background-position: right center;
        }
        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2), 0 0 15px rgba(56, 189, 248, 0.5);
        }
        [x-cloak] { display: none !important; }

        .spinner {
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 2px solid #38BDF8;
            width: 16px;
            height: 16px;
            animation: spin 1s linear infinite;
        }
        
        .animate-blob {
            animation: blob 7s infinite;
        }
        .animation-delay-2000 { animation-delay: -2s; }
        .animation-delay-4000 { animation-delay: -4s; }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        @keyframes blob {
	        0% { transform: translate(0px, 0px) scale(1); }
	        33% { transform: translate(30px, -50px) scale(1.1); }
	        66% { transform: translate(-20px, 20px) scale(0.9); }
	        100% { transform: translate(0px, 0px) scale(1); }
        }
    </style>
    <script src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.x.x/dist/alpine.min.js" defer></script>
</head>

<body x-data="appState()" @keydown.escape.window="showLoginModal = false; showSignupModal = false;">

    <div class="absolute top-0 left-0 -z-10 w-full h-screen overflow-hidden">
        <div class="absolute top-0 -left-4 w-96 h-96 bg-sky-500/20 rounded-full mix-blend-screen filter blur-3xl opacity-50 animate-blob"></div>
        <div class="absolute top-0 -right-4 w-96 h-96 bg-indigo-500/20 rounded-full mix-blend-screen filter blur-3xl opacity-50 animate-blob animation-delay-2000"></div>
        <div class="absolute -bottom-8 left-20 w-96 h-96 bg-purple-500/20 rounded-full mix-blend-screen filter blur-3xl opacity-50 animate-blob animation-delay-4000"></div>
    </div>

    <header class="fixed top-0 left-0 w-full z-50 glass-effect">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <a @click.prevent="page = 'home'" href="#" class="text-2xl font-bold gradient-text">1AItoro</a>
            <nav class="hidden md:flex items-center space-x-8">
                <a @click.prevent="page = 'home'" href="#" class="hover:text-sky-400 transition-colors">Home</a>
                <a @click.prevent="page = 'marketing'" href="#" class="hover:text-sky-400 transition-colors">AI Marketing</a>
                <a @click.prevent="page = 'finance'" href="#" class="hover:text-sky-400 transition-colors">AI Finance</a>
                <a @click.prevent="page = 'pricing'" href="#" class="hover:text-sky-400 transition-colors">Pricing</a>
                <a @click.prevent="page = 'referral'" href="#" class="hover:text-sky-400 transition-colors">Referrals</a>
            </nav>
            <div class="hidden md:flex items-center space-x-4">
                <button @click="showLoginModal = true" class="hover:text-sky-400 transition-colors">Log In</button>
                <button @click="showSignupModal = true" class="cta-button text-white font-bold py-2 px-4 rounded-lg">
                    Get Started
                </button>
            </div>
            <div class="md:hidden">
                <button @click="isMenuOpen = !isMenuOpen">
                    <i class="ph-list text-3xl"></i>
                </button>
            </div>
        </div>
        <div x-show="isMenuOpen" @click.away="isMenuOpen = false" class="md:hidden glass-effect" x-cloak>
             <nav class="flex flex-col items-center py-4 space-y-4">
                <a @click.prevent="page = 'home'; isMenuOpen = false" href="#" class="hover:text-sky-400 transition-colors w-full text-center py-2">Home</a>
                <a @click.prevent="page = 'marketing'; isMenuOpen = false" href="#" class="hover:text-sky-400 transition-colors w-full text-center py-2">AI Marketing</a>
                <a @click.prevent="page = 'finance'; isMenuOpen = false" href="#" class="hover:text-sky-400 transition-colors w-full text-center py-2">AI Finance</a>
                <a @click.prevent="page = 'pricing'; isMenuOpen = false" href="#" class="hover:text-sky-400 transition-colors w-full text-center py-2">Pricing</a>
                <a @click.prevent="page = 'referral'; isMenuOpen = false" href="#" class="hover:text-sky-400 transition-colors w-full text-center py-2">Referrals</a>
                <button @click="showLoginModal = true; isMenuOpen = false" class="hover:text-sky-400 transition-colors w-full py-2">Log In</button>
                <button @click="showSignupModal = true; isMenuOpen = false" class="cta-button text-white font-bold py-2 px-6 rounded-lg w-3/4 mx-auto">
                    Get Started
                </button>
            </nav>
        </div>
    </header>

    <main class="pt-24 min-h-screen">
        <div x-show="page === 'home'" x-cloak>
            <section id="home" class="container mx-auto px-6 py-16 text-center">
                <h1 class="text-4xl md:text-6xl font-extrabold leading-tight">
                    Gain Your <span class="gradient-text">Unfair Advantage</span> with AI
                </h1>
                <p class="mt-4 text-lg md:text-xl text-slate-400 max-w-3xl mx-auto">
                    1AItoro leverages cutting-edge artificial intelligence to deliver predictive insights for marketing, finance, and crypto. Stop guessing, start winning.
                </p>
                <div class="mt-8 flex justify-center space-x-4">
                    <button @click.prevent="page = 'pricing'" class="cta-button text-white font-bold py-3 px-8 rounded-lg text-lg">
                        View Pricing
                    </button>
                    <button @click.prevent="page = 'marketing'" class="glass-effect py-3 px-8 rounded-lg text-lg hover:bg-slate-700/50 transition">
                        Explore Tools
                    </button>
                </div>
            </section>

            <section class="container mx-auto px-6 py-16">
                <h2 class="text-3xl font-bold text-center mb-12">One Platform, Infinite Possibilities</h2>
                <div class="grid md:grid-cols-3 gap-8">
                    <div @click="page = 'marketing'" class="feature-card glass-effect rounded-2xl p-8 cursor-pointer transition-all duration-300">
                        <div class="p-3 bg-sky-500/20 rounded-lg inline-block">
                            <i class="ph-projector-screen-chart text-sky-400 text-3xl"></i>
                        </div>
                        <h3 class="text-2xl font-bold mt-4">AI Marketing</h3>
                        <p class="mt-2 text-slate-400">Automate content, optimize ad spend, and uncover deep customer insights to supercharge your growth.</p>
                    </div>
                    <div @click="page = 'finance'" class="feature-card glass-effect rounded-2xl p-8 cursor-pointer transition-all duration-300">
                        <div class="p-3 bg-indigo-500/20 rounded-lg inline-block">
                            <i class="ph-chart-line text-indigo-400 text-3xl"></i>
                        </div>
                        <h3 class="text-2xl font-bold mt-4">AI Finance & Crypto</h3>
                        <p class="mt-2 text-slate-400">Leverage predictive models for stocks and crypto. Get Wall Street-grade AI analysis before the market moves.</p>
                    </div>
                    <div @click="page = 'pricing'" class="feature-card glass-effect rounded-2xl p-8 cursor-pointer transition-all duration-300">
                        <div class="p-3 bg-purple-500/20 rounded-lg inline-block">
                            <i class="ph-rocket-launch text-purple-400 text-3xl"></i>
                        </div>
                        <h3 class="text-2xl font-bold mt-4">Profit From The Edge</h3>
                        <p class="mt-2 text-slate-400">Our service pays for itself. Use our insights to increase your profits, and benefit from our generous referral program.</p>
                    </div>
                </div>
            </section>
        </div>

        <div x-show="page === 'marketing'" x-cloak>
            <div x-data="marketingPageState()">
                <section class="container mx-auto px-6 py-16">
                    <div class="text-center max-w-3xl mx-auto">
                        <h1 class="text-4xl md:text-5xl font-extrabold"><span class="gradient-text">AI-Powered Marketing</span> Suite</h1>
                        <p class="mt-4 text-lg text-slate-400">Go beyond vanity metrics. Drive real results with intelligent automation and predictive analytics that understand your customers.</p>
                    </div>

                    <div class="mt-16 glass-effect rounded-2xl p-8 max-w-4xl mx-auto">
                        <h2 class="text-2xl font-bold text-center mb-6 flex items-center justify-center"><span class="gradient-text mr-3">✨</span> Ad Copy Generator</h2>
                        <div class="grid sm:grid-cols-2 gap-6">
                            <div>
                                <label for="productName" class="block text-sm font-medium text-slate-300">Product Name</label>
                                <input type="text" id="productName" x-model="adCopy.productName" placeholder="e.g., QuantumLeap CRM" class="w-full mt-1 p-3 bg-slate-800 border border-slate-700 rounded-lg focus:ring-2 focus:ring-sky-500 focus:outline-none">
                            </div>
                            <div>
                                <label for="productDesc" class="block text-sm font-medium text-slate-300">Product Description</label>
                                <input type="text" id="productDesc" x-model="adCopy.productDesc" placeholder="e.g., An AI-powered sales platform" class="w-full mt-1 p-3 bg-slate-800 border border-slate-700 rounded-lg focus:ring-2 focus:ring-sky-500 focus:outline-none">
                            </div>
                        </div>
                        <button @click="generateAdCopy()" :disabled="adCopy.loading" class="mt-6 w-full cta-button text-white font-bold py-3 px-6 rounded-lg flex items-center justify-center disabled:opacity-50 disabled:cursor-not-allowed">
                            <div x-show="adCopy.loading" class="spinner mr-2"></div>
                            <span x-text="adCopy.loading ? 'Generating...' : 'Generate Ad Copy'"></span>
                        </button>
                        <div x-show="adCopy.result" class="mt-6 p-4 bg-slate-800/50 rounded-lg border border-slate-700" x-cloak>
                            <h4 class="font-semibold mb-2">Generated Copy:</h4>
                            <p class="text-slate-300 whitespace-pre-wrap" x-text="adCopy.result"></p>
                        </div>
                    </div>

                    <div class="mt-12 glass-effect rounded-2xl p-8 max-w-4xl mx-auto">
                        <h2 class="text-2xl font-bold text-center mb-6 flex items-center justify-center"><span class="gradient-text mr-3">✨</span> Market Trend Analyzer</h2>
                        <label for="marketTopic" class="block text-sm font-medium text-slate-300">Market Topic</label>
                        <input type="text" id="marketTopic" x-model="trends.topic" placeholder="e.g., The future of remote work" class="w-full mt-1 p-3 bg-slate-800 border border-slate-700 rounded-lg focus:ring-2 focus:ring-sky-500 focus:outline-none">
                        <button @click="analyzeTrends()" :disabled="trends.loading" class="mt-6 w-full cta-button text-white font-bold py-3 px-6 rounded-lg flex items-center justify-center disabled:opacity-50 disabled:cursor-not-allowed">
                            <div x-show="trends.loading" class="spinner mr-2"></div>
                            <span x-text="trends.loading ? 'Analyzing...' : 'Analyze Market Trends'"></span>
                        </button>
                        <div x-show="trends.result" class="mt-6 p-4 bg-slate-800/50 rounded-lg border border-slate-700" x-cloak>
                            <h4 class="font-semibold mb-2">Trend Analysis:</h4>
                            <p class="text-slate-300 whitespace-pre-wrap" x-text="trends.result"></p>
                        </div>
                    </div>
                </section>
            </div>
        </div>

        <div x-show="page === 'finance'" x-cloak>
             <div x-data="financePageState()">
                <section class="container mx-auto px-6 py-16">
                     <div class="text-center max-w-3xl mx-auto">
                        <h1 class="text-4xl md:text-5xl font-extrabold">AI <span class="gradient-text">Finance & Crypto</span> Predictions</h1>
                        <p class="mt-4 text-lg text-slate-400">Access institutional-grade AI analysis for the stock and crypto markets. Make data-driven decisions, not emotional ones.</p>
                    </div>
                    
                     <div class="mt-16 glass-effect rounded-2xl p-8 max-w-4xl mx-auto">
                        <h2 class="text-2xl font-bold text-center mb-6 flex items-center justify-center"><span class="gradient-text mr-3">✨</span> Real-Time Asset Sentiment</h2>
                        <label for="asset" class="block text-sm font-medium text-slate-300">Stock Ticker or Crypto</label>
                        <input type="text" id="asset" x-model="sentiment.asset" placeholder="e.g., TSLA or Bitcoin" class="w-full mt-1 p-3 bg-slate-800 border border-slate-700 rounded-lg focus:ring-2 focus:ring-sky-500 focus:outline-none">
                        <button @click="getSentiment()" :disabled="sentiment.loading" class="mt-6 w-full cta-button text-white font-bold py-3 px-6 rounded-lg flex items-center justify-center disabled:opacity-50 disabled:cursor-not-allowed">
                             <div x-show="sentiment.loading" class="spinner mr-2"></div>
                            <span x-text="sentiment.loading ? 'Analyzing Sentiment...' : 'Get AI Sentiment Analysis'"></span>
                        </button>
                         <div x-show="sentiment.result" class="mt-6 p-4 bg-slate-800/50 rounded-lg border border-slate-700" x-cloak>
                            <h4 class="font-semibold mb-2" x-text="`Sentiment Analysis for ${sentiment.analyzedAsset}`"></h4>
                            <p class="text-slate-300 whitespace-pre-wrap" x-text="sentiment.result"></p>
                        </div>
                    </div>
                </section>
            </div>
        </div>

        <div x-show="page === 'pricing'" x-cloak>
            <div x-data="pricingState()">
                <section class="container mx-auto px-6 py-16">
                    <div class="text-center max-w-3xl mx-auto">
                        <h1 class="text-4xl md:text-5xl font-extrabold">Choose Your <span class="gradient-text">Winning Plan</span></h1>
                        <p class="mt-4 text-lg text-slate-400">Start for free, then scale as you grow. All plans come with a 14-day free trial. Cancel anytime.</p>
                    </div>

                    <div class="mt-8 flex justify-center items-center space-x-4">
                        <span :class="{ 'text-sky-400': billing === 'monthly' }" class="font-semibold">Monthly</span>
                        <label class="relative inline-flex items-center cursor-pointer">
                            <input type="checkbox" class="sr-only peer" @change="billing = billing === 'monthly' ? 'yearly' : 'monthly'">
                            <div class="w-14 h-8 bg-slate-700 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[4px] after:left-[4px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-6 after:w-6 after:transition-all peer-checked:bg-sky-500"></div>
                        </label>
                        <span :class="{ 'text-sky-400': billing === 'yearly' }" class="font-semibold">Yearly (Save 20%)</span>
                    </div>

                    <div class="mt-12 grid md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto items-start">
                        <div class="glass-effect rounded-2xl p-8 border-2 border-slate-700 flex flex-col h-full">
                            <h3 class="text-2xl font-bold">Starter</h3>
                            <p class="mt-2 text-slate-400">For individuals and enthusiasts getting started with AI.</p>
                            <div class="mt-6">
                                <span class="text-4xl font-extrabold" x-text="billing === 'monthly' ? '$49' : '$39'"></span>
                                <span class="text-slate-400" x-text="billing === 'monthly' ? '/ month' : '/ mo (billed annually)'"></span>
                            </div>
                            <ul class="my-8 space-y-4 text-slate-300 flex-grow">
                                <li class="flex items-center"><i class="ph-check-circle text-green-400 mr-2 text-xl"></i> Basic AI Marketing Tools</li>
                                <li class="flex items-center"><i class="ph-check-circle text-green-400 mr-2 text-xl"></i> Basic Finance & Crypto Signals</li>
                                <li class="flex items-center"><i class="ph-check-circle text-green-400 mr-2 text-xl"></i> 100 Content Generations/mo</li>
                                <li class="flex items-center"><i class="ph-check-circle text-green-400 mr-2 text-xl"></i> Standard Support</li>
                            </ul>
                            <button @click="checkout('starter')" class="w-full mt-auto py-3 px-6 rounded-lg bg-slate-700 hover:bg-slate-600 transition">Start 14-Day Trial</button>
                        </div>
                        
                        <div class="glass-effect rounded-2xl p-8 border-2 border-sky-500 relative flex flex-col h-full">
                            <div class="absolute top-0 -translate-y-1/2 left-1/2 -translate-x-1/2 px-4 py-1 bg-sky-500 text-white text-sm font-bold rounded-full">MOST POPULAR</div>
                            <h3 class="text-2xl font-bold">Pro</h3>
                            <p class="mt-2 text-slate-400">For professionals and businesses who need to win.</p>
                            <div class="mt-6">
                                <span class="text-4xl font-extrabold" x-text="billing === 'monthly' ? '$99' : '$79'"></span>
                          
