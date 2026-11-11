<template>
  <main class="min-h-screen bg-gray-50 py-10 px-4 font-sans">
    <div class="max-w-6xl mx-auto">
      
      <!-- Header Section -->
      <header class="text-center mb-10">
        <h1 class="text-4xl font-extrabold text-gray-900 mb-2">Beauhurst AI SEO Blog Generator</h1>
        <p class="text-lg text-gray-600">Transforming company datasets into SEO-optimised industry reports using Nuxt.</p>
      </header>

      <!-- Upload Box -->
      <div class="bg-white shadow rounded-lg p-6 mb-8 border border-gray-200 text-center">
        <label class="block text-sm font-medium text-gray-700 mb-2">Upload Industry CSV Dataset</label>
        <input 
          type="file" 
          accept=".csv" 
          @change="handleFileUpload" 
          class="block mx-auto text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100 cursor-pointer"
        />
      </div>

      <!-- Generated Blog Content -->
      <div v-if="blogGenerated" class="space-y-8">
        
        <!-- Blog Header & SEO Meta Info -->
        <article class="bg-white shadow-md rounded-xl p-8 border border-gray-200">
          <div class="mb-4">
            <span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded">SEO Optimized Report</span>
            <span class="text-xs text-gray-400 ml-2">Meta Description: {{ seoMetaDescription }}</span>
          </div>

          <h2 class="text-3xl font-bold text-gray-900 mb-4">{{ blogTitle }}</h2>
          <p class="text-gray-700 text-lg leading-relaxed mb-6">{{ blogIntro }}</p>

          <!-- Key Statistics Grid -->
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
            <div class="bg-blue-50 p-4 rounded-lg border border-blue-100">
              <p class="text-sm text-blue-600 font-medium">Total Funding Raised</p>
              <p class="text-2xl font-bold text-blue-900">£{{ totalFundingFormatted }}</p>
            </div>
            <div class="bg-emerald-50 p-4 rounded-lg border border-emerald-100">
              <p class="text-sm text-emerald-600 font-medium">Top Hub</p>
              <p class="text-2xl font-bold text-emerald-900">{{ topRegion }} ({{ topRegionCount }} companies)</p>
            </div>
            <div class="bg-purple-50 p-4 rounded-lg border border-purple-100">
              <p class="text-sm text-purple-600 font-medium">Companies Analyzed</p>
              <p class="text-2xl font-bold text-purple-900">{{ companies.length }}</p>
            </div>
          </div>

          <!-- Commentary / Body -->
          <div class="prose max-w-none text-gray-700 space-y-4" v-html="aiContent"></div>
        </article>

        <!-- Ranking Table -->
        <div class="bg-white shadow-md rounded-xl overflow-hidden border border-gray-200">
          <div class="px-6 py-4 bg-gray-100 border-b border-gray-200">
            <h3 class="text-xl font-bold text-gray-800">Top Companies Ranking Table</h3>
          </div>
          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200 text-left text-sm">
              <thead class="bg-gray-50 text-gray-600 font-semibold">
                <tr>
                  <th class="px-6 py-3">Rank</th>
                  <th class="px-6 py-3">Company</th>
                  <th class="px-6 py-3">Region</th>
                  <th class="px-6 py-3">Stage</th>
                  <th class="px-6 py-3">Total Raised</th>
                  <th class="px-6 py-3">Website</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200 bg-white">
                <tr v-for="company in companies" :key="company.Rank" class="hover:bg-gray-50">
                  <td class="px-6 py-4 font-bold text-gray-900">#{{ company.Rank }}</td>
                  <td class="px-6 py-4 font-semibold text-blue-600">{{ company.Company }}</td>
                  <td class="px-6 py-4 text-gray-600">{{ company.Region }}</td>
                  <td class="px-6 py-4">
                    <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded">{{ company.Stage }}</span>
                  </td>
                  <td class="px-6 py-4 font-medium text-gray-900">{{ company['Total Raised'] }}</td>
                  <td class="px-6 py-4">
                    <a :href="company.Website" target="_blank" class="text-blue-500 hover:underline">Visit</a>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

      </div>

    </div>
  </main>
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
        <p><strong>Key Industry Takeaway:</strong> ${maxReg} remains the undisputed epicenter of innovation, housing ${maxCount} out of the top ${data.length} ranked enterprises.</p>
        <p>Ventures across application software and core services are capturing significant investor attention, laying the groundwork for future market leaders.</p>
      `

      blogGenerated.value = true
    }
  })
}
</script>