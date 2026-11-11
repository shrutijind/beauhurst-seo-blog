<template>
  <div class="min-h-screen bg-slate-900 font-sans text-slate-100 antialiased selection:bg-blue-600 selection:text-white">
    <!-- Top Executive Brand Bar -->
    <header class="bg-slate-950 border-b border-slate-800 py-5 px-8 sticky top-0 z-50 shadow-lg backdrop-blur-md bg-opacity-90">
      <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center">
        <div class="flex items-center space-x-3">
          <div class="bg-gradient-to-tr from-blue-600 to-indigo-500 text-white font-black px-3 py-1.5 rounded-xl text-sm shadow-md tracking-wide">
            BEAUHURST
          </div>
          <div>
            <h1 class="text-lg font-bold tracking-tight text-white flex items-center gap-2">
              AI SEO Blog & Intelligence Engine
              <span class="text-xs uppercase bg-blue-500/20 text-blue-400 font-semibold px-2 py-0.5 rounded-full border border-blue-500/30">v2.0</span>
            </h1>
          </div>
        </div>
        <div class="text-xs text-slate-400 mt-2 sm:mt-0 flex items-center gap-2">
          <span class="inline-block w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
          Nuxt 3 • Tailwind CSS • Papa Parse Active
        </div>
      </div>
    </header>

    <main class="max-w-7xl mx-auto py-12 px-4 sm:px-6 lg:px-8">
      
      <!-- Interactive Upload Hero Card -->
      <div class="bg-slate-800/60 backdrop-blur rounded-2xl shadow-2xl border border-slate-700/80 p-8 mb-10 text-center relative overflow-hidden transition-all hover:border-blue-500/50">
        <div class="absolute -right-20 -top-20 w-64 h-64 bg-blue-600/10 rounded-full blur-3xl pointer-events-none"></div>
        <div class="absolute -left-20 -bottom-20 w-64 h-64 bg-emerald-600/10 rounded-full blur-3xl pointer-events-none"></div>

        <div class="max-w-xl mx-auto relative z-10">
          <h2 class="text-3xl font-extrabold text-white mb-3 tracking-tight">Upload Market Dataset</h2>
          <p class="text-sm text-slate-400 mb-6">Import your company CSV feed to automatically trigger predictive SEO articles, metric aggregations, and leadership rankings.</p>
          
          <label class="group flex flex-col items-center justify-center border-2 border-dashed border-slate-600 rounded-2xl p-8 bg-slate-900/50 hover:bg-slate-900/80 hover:border-blue-500 cursor-pointer transition-all duration-300">
            <div class="w-12 h-12 rounded-full bg-blue-500/10 flex items-center justify-center text-blue-400 mb-3 group-hover:scale-110 transition-transform">
              <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"/>
              </svg>
            </div>
            <span class="text-sm font-semibold text-slate-200 group-hover:text-blue-400 transition-colors">Click to upload CSV dataset</span>
            <span class="text-xs text-slate-500 mt-1">Supports standard CSV exports (e.g., fintech_companies_seed.csv)</span>
            <input type="file" accept=".csv" @change="handleFileUpload" class="hidden" />
          </label>
        </div>
      </div>

      <!-- Generated Report Dashboard -->
      <div v-if="blogGenerated" class="space-y-8 animate-fade-in">
        
        <!-- Key Metrics Cards Grid -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="bg-slate-800/80 backdrop-blur p-6 rounded-2xl shadow-lg border border-slate-700/80 relative overflow-hidden">
            <div class="absolute top-0 right-0 transform translate-x-3 -translate-y-3 w-20 h-20 bg-blue-500/10 rounded-full blur-xl"></div>
            <p class="text-xs font-bold text-blue-400 uppercase tracking-widest mb-1">Total Funding Raised</p>
            <p class="text-3xl font-black text-white tracking-tight">£{{ totalFundingFormatted }}</p>
            <span class="text-xs text-slate-400 mt-2 block font-medium">Aggregated active portfolio volume</span>
          </div>

          <div class="bg-slate-800/80 backdrop-blur p-6 rounded-2xl shadow-lg border border-slate-700/80 relative overflow-hidden">
            <div class="absolute top-0 right-0 transform translate-x-3 -translate-y-3 w-20 h-20 bg-emerald-500/10 rounded-full blur-xl"></div>
            <p class="text-xs font-bold text-emerald-400 uppercase tracking-widest mb-1">Top Regional Hub</p>
            <p class="text-3xl font-black text-white tracking-tight">{{ topRegion }}</p>
            <span class="text-xs text-emerald-400/90 font-semibold mt-2 block">{{ topRegionCount }} verified enterprises concentrated here</span>
          </div>

          <div class="bg-slate-800/80 backdrop-blur p-6 rounded-2xl shadow-lg border border-slate-700/80 relative overflow-hidden">
            <div class="absolute top-0 right-0 transform translate-x-3 -translate-y-3 w-20 h-20 bg-purple-500/10 rounded-full blur-xl"></div>
            <p class="text-xs font-bold text-purple-400 uppercase tracking-widest mb-1">Dataset Coverage</p>
            <p class="text-3xl font-black text-white tracking-tight">{{ companies.length }}</p>
            <span class="text-xs text-slate-400 mt-2 block font-medium">High-growth companies analyzed</span>
          </div>
        </div>

        <!-- SEO Blog Article Section -->
        <article class="bg-slate-800/80 backdrop-blur rounded-2xl shadow-xl border border-slate-700/80 p-8 sm:p-10">
          <div class="flex flex-wrap items-center gap-3 mb-6">
            <span class="bg-blue-600/20 text-blue-300 border border-blue-500/30 text-xs font-semibold px-3.5 py-1.5 rounded-full">
              AI SEO Optimized Report
            </span>
            <span class="text-xs text-slate-400 bg-slate-900/60 px-3.5 py-1.5 rounded-full border border-slate-700">
              Meta Description: {{ seoMetaDescription }}
            </span>
          </div>

          <h2 class="text-3xl sm:text-4xl font-black text-white mb-6 tracking-tight leading-tight">{{ blogTitle }}</h2>
          <p class="text-lg text-slate-300 leading-relaxed mb-8 font-normal">{{ blogIntro }}</p>

          <!-- Commentary / Body -->
          <div class="prose prose-invert max-w-none text-slate-300 space-y-4 border-t border-slate-700/80 pt-6 leading-relaxed" v-html="aiContent"></div>
        </article>

        <!-- Ranking Leaderboard Table -->
        <div class="bg-slate-800/80 backdrop-blur rounded-2xl shadow-xl border border-slate-700/80 overflow-hidden">
          <div class="px-6 py-5 bg-slate-900/60 border-b border-slate-700 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2">
            <h3 class="font-bold text-white text-lg flex items-center gap-2">
              <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/>
              </svg>
              Top Ranked Companies Leaderboard
            </h3>
            <span class="text-xs text-slate-400 bg-slate-800 px-3 py-1 rounded-lg border border-slate-700">Sorted by funding volume & ranking</span>
          </div>

          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-slate-700/80 text-left text-sm">
              <thead class="bg-slate-900/30 text-slate-400 uppercase font-bold text-xs tracking-wider">
                <tr>
                  <th class="px-6 py-4">Rank</th>
                  <th class="px-6 py-4">Company</th>
                  <th class="px-6 py-4">Region</th>
                  <th class="px-6 py-4">Stage</th>
                  <th class="px-6 py-4">Total Raised</th>
                  <th class="px-6 py-4 text-right">Website</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-slate-700/50 bg-slate-800/40">
                <tr v-for="company in companies" :key="company.Rank" class="hover:bg-slate-700/50 transition-colors">
                  <td class="px-6 py-4 font-extrabold text-blue-400">#{{ company.Rank }}</td>
                  <td class="px-6 py-4 font-bold text-white">{{ company.Company }}</td>
                  <td class="px-6 py-4 text-slate-300 font-medium">{{ company.Region }}</td>
                  <td class="px-6 py-4">
                    <span class="bg-slate-900/80 text-slate-300 border border-slate-700 font-semibold text-xs px-3 py-1 rounded-full shadow-sm">{{ company.Stage }}</span>
                  </td>
                  <td class="px-6 py-4 font-bold text-emerald-400">{{ company['Total Raised'] }}</td>
                  <td class="px-6 py-4 text-right">
                    <a :href="company.Website" target="_blank" class="inline-flex items-center gap-1 text-xs font-bold text-white bg-blue-600 hover:bg-blue-500 px-3.5 py-1.5 rounded-lg shadow transition-all">
                      Visit →
                    </a>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

      </div>

    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Papa from 'papaparse'

const blogGenerated = ref(false)
const companies = ref([])
const blogTitle = ref('')
const seoMetaDescription = ref('')
const blogIntro = ref('')
const aiContent = ref('')
const totalFundingFormatted = ref('0')
const topRegion = ref('')
const topRegionCount = ref(0)

const handleFileUpload = (event) => {
  const file = event.target.files[0]
  if (!file) return

  Papa.parse(file, {
    header: true,
    skipEmptyLines: true,
    complete: (results) => {
      const data = results.data
      companies.value = data

      // 1. Calculate statistics programmatically
      let totalSum = 0
      const regionCounts = {}

      data.forEach(row => {
        const rawVal = row['Total Raised'] || '£0'
        const num = parseFloat(rawVal.replace('£', '').replace(/,/g, '').trim()) || 0
        totalSum += num

        const reg = row['Region'] || 'Unknown'
        regionCounts[reg] = (regionCounts[reg] || 0) + 1
      })

      totalFundingFormatted.value = totalSum.toLocaleString()

      // Find top region
      let maxReg = ''
      let maxCount = 0
      for (const [reg, count] of Object.entries(regionCounts)) {
        if (count > maxCount) {
          maxCount = count
          maxReg = reg
        }
      }
      topRegion.value = maxReg
      topRegionCount.value = maxCount

      // 2. Set Blog content
      blogTitle.value = `UK Market Report: Top ${data.length} Companies & Funding Insights`
      seoMetaDescription.value = `Discover top performing companies, funding totals, and regional breakdown in our comprehensive market analysis.`
      blogIntro.value = `This sector continues to demonstrate remarkable resilience and innovation. This report examines the top ${data.length} companies, tracking a combined fundraising volume of £${totalFundingFormatted.value}.`
      
      aiContent.value = `
        <p class="leading-relaxed"><strong>Key Industry Takeaway:</strong> ${maxReg} remains the undisputed epicenter of innovation, housing ${maxCount} out of the top ${data.length} ranked enterprises.</p>
        <p class="leading-relaxed">Ventures across application software, data intelligence, and core financial services are capturing significant investor attention, laying the groundwork for future market leaders.</p>
      `

      blogGenerated.value = true
    }
  })
}
</script>q