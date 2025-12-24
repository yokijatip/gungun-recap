<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50 p-8">
    <div class="max-w mx-auto">
      <!-- Header -->
      <div class="text-center mb-12">
        <div class="inline-flex items-center justify-center w-16 h-16 bg-blue-600 rounded-2xl mb-4">
          <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
        </div>
        <h1 class="text-4xl font-bold text-slate-900">
          Rekap Dokumentasi Service AC
        </h1>
        <br/>
        <p class="text-sm font-semibold">
          by Yoki J Perkasa
        </p>

        <p class="text-lg text-slate-600 max-w-2xl mx-auto">
          Pilih template dokumentasi yang sesuai dengan kebutuhan project Anda
        </p>
      </div>

      <!-- Template Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-8">
        <!-- Template 1: Standard Service -->
        <div
            @click="selectTemplate('standard')"
            class="bg-white rounded-xl shadow-md hover:shadow-xl transition-all duration-300 cursor-pointer border-2 border-transparent hover:border-blue-500 overflow-hidden group"
        >
          <div class="bg-gradient-to-br from-blue-500 to-blue-600 p-6 text-white">
            <div class="flex items-center justify-between mb-4">
              <h3 class="text-xl font-bold">Standard Service</h3>
              <div class="w-10 h-10 bg-white/20 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
                </svg>
              </div>
            </div>
            <p class="text-blue-100 text-sm">
              Template standar untuk dokumentasi service AC rutin
            </p>
          </div>

          <div class="p-6">
            <div class="space-y-3">
              <div class="flex items-center text-sm text-slate-600">
                <svg class="w-5 h-5 text-green-500 mr-2" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                Foto Lokasi, Proses, Sebelum, Sesudah
              </div>
              <div class="flex items-center text-sm text-slate-600">
                <svg class="w-5 h-5 text-green-500 mr-2" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                7 baris per halaman
              </div>
              <div class="flex items-center text-sm text-slate-600">
                <svg class="w-5 h-5 text-green-500 mr-2" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                Uraian kegiatan checklist
              </div>
              <div class="flex items-center text-sm text-slate-600">
                <svg class="w-5 h-5 text-green-500 mr-2" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                Export PDF & Excel
              </div>
            </div>

            <button class="mt-6 w-full bg-blue-600 text-white py-3 rounded-lg font-semibold hover:bg-blue-700 transition-colors group-hover:shadow-lg">
              Pilih Template
            </button>
          </div>
        </div>

        <!-- Template 2: Custom (Coming Soon) -->
        <div class="bg-white rounded-xl shadow-md overflow-hidden border-2 border-dashed border-slate-300 opacity-60 cursor-not-allowed">
          <div class="bg-gradient-to-br from-slate-400 to-slate-500 p-6 text-white">
            <div class="flex items-center justify-between mb-4">
              <h3 class="text-xl font-bold">Custom Template</h3>
              <div class="w-10 h-10 bg-white/20 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                </svg>
              </div>
            </div>
            <p class="text-slate-100 text-sm">
              Buat template sesuai kebutuhan Anda
            </p>
          </div>

          <div class="p-6">
            <div class="flex items-center justify-center py-8">
              <span class="text-sm text-slate-500 font-medium">Segera Hadir</span>
            </div>

            <button disabled class="mt-6 w-full bg-slate-300 text-slate-500 py-3 rounded-lg font-semibold cursor-not-allowed">
              Coming Soon
            </button>
          </div>
        </div>

        <!-- Template 3: Another Template (Coming Soon) -->
        <div class="bg-white rounded-xl shadow-md overflow-hidden border-2 border-dashed border-slate-300 opacity-60 cursor-not-allowed">
          <div class="bg-gradient-to-br from-slate-400 to-slate-500 p-6 text-white">
            <div class="flex items-center justify-between mb-4">
              <h3 class="text-xl font-bold">Template Lainnya</h3>
              <div class="w-10 h-10 bg-white/20 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01" />
                </svg>
              </div>
            </div>
            <p class="text-slate-100 text-sm">
              Template dengan format berbeda
            </p>
          </div>

          <div class="p-6">
            <div class="flex items-center justify-center py-8">
              <span class="text-sm text-slate-500 font-medium">Segera Hadir</span>
            </div>

            <button disabled class="mt-6 w-full bg-slate-300 text-slate-500 py-3 rounded-lg font-semibold cursor-not-allowed">
              Coming Soon
            </button>
          </div>
        </div>
      </div>

      <!-- Info Banner -->
      <div class="bg-blue-50 border border-blue-200 rounded-xl p-6">
        <div class="flex items-start gap-4">
          <div class="flex-shrink-0">
            <svg class="w-6 h-6 text-blue-600" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
            </svg>
          </div>
          <div class="flex-1">
            <h4 class="text-blue-900 font-semibold mb-1">Fitur Utama Aplikasi</h4>
            <ul class="text-blue-800 text-sm space-y-1">
              <li>• Upload foto dengan auto-resize ke ukuran 1:1 (kotak) untuk konsistensi</li>
              <li>• Checkbox uraian kegiatan dengan fitur "Check All"</li>
              <li>• Export ke PDF dan Excel dengan satu klik</li>
              <li>• Preview sebelum export untuk memastikan hasil sempurna</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['select-template']);

const selectTemplate = (templateType) => {
  emit('select-template', templateType);
};
</script>
