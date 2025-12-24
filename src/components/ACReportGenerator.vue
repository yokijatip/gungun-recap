<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50 p-6">
    <div class=" mx-auto">
      <!-- Header with Back Button -->
      <div class="mb-6 flex items-center gap-4">
        <button
            @click="$emit('back')"
            class="flex items-center gap-2 text-slate-600 hover:text-slate-900 font-medium transition-colors"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
          </svg>
          Kembali
        </button>
      </div>

      <!-- Main Header -->
      <div class="bg-white rounded-xl shadow-md p-8 mb-6">
        <div class="flex items-center gap-4 mb-6">
          <div class="w-12 h-12 bg-blue-600 rounded-xl flex items-center justify-center">
            <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
          </div>
          <div>
            <h1 class="text-3xl font-bold text-slate-900">
              Generator Laporan Service AC
            </h1>
            <p class="text-slate-600 mt-1">
              {{ dynamicTitle }}
            </p>
          </div>
        </div>

        <!-- Info Inputs -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div>
            <label class="block text-sm font-semibold text-slate-700 mb-2">
              Nama Gedung / Lokasi
            </label>
            <input
                v-model="buildingName"
                type="text"
                class="w-full px-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all"
                placeholder="Contoh: KANTOR GEDUNG DITJEN IMIGRASI"
            />
          </div>

          <div>
            <label class="block text-sm font-semibold text-slate-700 mb-2">
              Periode
            </label>
            <input
                v-model="period"
                type="text"
                class="w-full px-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all"
                placeholder="Contoh: September 2025"
            />
          </div>
        </div>
      </div>

      <!-- Entry Form -->
      <div class="bg-white rounded-xl shadow-md p-8 mb-6">
        <h2 class="text-2xl font-bold text-slate-900 mb-6 flex items-center gap-2">
          <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
          </svg>
          Tambah Data Service
        </h2>

        <!-- Added lokasi field -->
        <div class="mb-6">
          <label class="block text-sm font-semibold text-slate-700 mb-2">
            Lokasi Spesifik
          </label>
          <input
              v-model="currentEntry.lokasi"
              type="text"
              class="w-full px-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all"
              placeholder="Contoh: Lantai 2 Ruang Meeting"
          />
        </div>

        <!-- Updated photo upload section with drag and drop capability and select all button -->
        <div class="mb-4 flex items-center justify-between">
          <h3 class="text-sm font-semibold text-slate-700">Foto Dokumentasi</h3>
          <button
              @click="selectAllPhotos"
              class="text-sm text-blue-600 hover:text-blue-700 font-medium flex items-center gap-1"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            {{ allPhotosSelected ? 'Bersihkan' : 'Pilih Semua' }}
          </button>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
          <!-- Added drag and drop functionality to photo upload -->
          <!-- Foto Lokasi -->
          <div
              @dragover.prevent="draggedOver = 'fotoLokasi'"
              @dragleave.prevent="draggedOver = null"
              @drop.prevent="handlePhotoDrop('fotoLokasi', $event)"
          >
            <label class="block text-sm font-semibold text-slate-700 mb-2">
              Foto Lokasi
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoLokasi', $event)"
                  multiple
                  class="hidden"
                  ref="fotoLokasiInput"
              />
              <button
                  @click="fotoLokasiInput.click()"
                  :class="[
                    'w-full aspect-square border-2 border-dashed rounded-lg transition-all flex flex-col items-center justify-center bg-slate-50',
                    draggedOver === 'fotoLokasi' ? 'border-blue-500 bg-blue-50' : 'border-slate-300 hover:border-blue-500 hover:bg-blue-50'
                  ]"
              >
                <svg class="w-10 h-10 text-slate-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-slate-500 font-medium">Upload</span>
              </button>
              <div v-if="currentEntry.fotoLokasi.length > 0" class="mt-4 grid grid-cols-2 sm:grid-cols-3 gap-2">
                <div v-for="(image, index) in currentEntry.fotoLokasi" :key="`foto-lokasi-${index}`" class="relative aspect-square rounded-lg overflow-hidden border border-slate-200 group cursor-move">
                  <img
                      :src="image"
                      class="w-full h-full object-cover"
                      alt="Foto Lokasi"
                      draggable="true"
                      @dragstart="startPhotoDrag('fotoLokasi', index, $event)"
                  />
                  <button
                      @click="removeImage('fotoLokasi', index)"
                      class="absolute top-1 right-1 bg-red-500 text-white p-1 rounded-full hover:bg-red-600 transition-colors opacity-0 group-hover:opacity-100"
                      type="button"
                  >
                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Foto Proses -->
          <div
              @dragover.prevent="draggedOver = 'fotoProses'"
              @dragleave.prevent="draggedOver = null"
              @drop.prevent="handlePhotoDrop('fotoProses', $event)"
          >
            <label class="block text-sm font-semibold text-slate-700 mb-2">
              Foto Proses
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoProses', $event)"
                  multiple
                  class="hidden"
                  ref="fotoProsesInput"
              />
              <button
                  @click="fotoProsesInput.click()"
                  :class="[
                    'w-full aspect-square border-2 border-dashed rounded-lg transition-all flex flex-col items-center justify-center bg-slate-50',
                    draggedOver === 'fotoProses' ? 'border-blue-500 bg-blue-50' : 'border-slate-300 hover:border-blue-500 hover:bg-blue-50'
                  ]"
              >
                <svg class="w-10 h-10 text-slate-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-slate-500 font-medium">Upload</span>
              </button>
              <div v-if="currentEntry.fotoProses.length > 0" class="mt-4 grid grid-cols-2 sm:grid-cols-3 gap-2">
                <div v-for="(image, index) in currentEntry.fotoProses" :key="`foto-proses-${index}`" class="relative aspect-square rounded-lg overflow-hidden border border-slate-200 group cursor-move">
                  <img
                      :src="image"
                      class="w-full h-full object-cover"
                      alt="Foto Proses"
                      draggable="true"
                      @dragstart="startPhotoDrag('fotoProses', index, $event)"
                  />
                  <button
                      @click="removeImage('fotoProses', index)"
                      class="absolute top-1 right-1 bg-red-500 text-white p-1 rounded-full hover:bg-red-600 transition-colors opacity-0 group-hover:opacity-100"
                      type="button"
                  >
                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Foto Sebelum -->
          <div
              @dragover.prevent="draggedOver = 'fotoSebelum'"
              @dragleave.prevent="draggedOver = null"
              @drop.prevent="handlePhotoDrop('fotoSebelum', $event)"
          >
            <label class="block text-sm font-semibold text-slate-700 mb-2">
              Foto Sebelum
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoSebelum', $event)"
                  multiple
                  class="hidden"
                  ref="fotoSebelumInput"
              />
              <button
                  @click="fotoSebelumInput.click()"
                  :class="[
                    'w-full aspect-square border-2 border-dashed rounded-lg transition-all flex flex-col items-center justify-center bg-slate-50',
                    draggedOver === 'fotoSebelum' ? 'border-blue-500 bg-blue-50' : 'border-slate-300 hover:border-blue-500 hover:bg-blue-50'
                  ]"
              >
                <svg class="w-10 h-10 text-slate-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-slate-500 font-medium">Upload</span>
              </button>
              <div v-if="currentEntry.fotoSebelum.length > 0" class="mt-4 grid grid-cols-2 sm:grid-cols-3 gap-2">
                <div v-for="(image, index) in currentEntry.fotoSebelum" :key="`foto-sebelum-${index}`" class="relative aspect-square rounded-lg overflow-hidden border border-slate-200 group cursor-move">
                  <img
                      :src="image"
                      class="w-full h-full object-cover"
                      alt="Foto Sebelum"
                      draggable="true"
                      @dragstart="startPhotoDrag('fotoSebelum', index, $event)"
                  />
                  <button
                      @click="removeImage('fotoSebelum', index)"
                      class="absolute top-1 right-1 bg-red-500 text-white p-1 rounded-full hover:bg-red-600 transition-colors opacity-0 group-hover:opacity-100"
                      type="button"
                  >
                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Foto Sesudah -->
          <div
              @dragover.prevent="draggedOver = 'fotoSesudah'"
              @dragleave.prevent="draggedOver = null"
              @drop.prevent="handlePhotoDrop('fotoSesudah', $event)"
          >
            <label class="block text-sm font-semibold text-slate-700 mb-2">
              Foto Sesudah
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoSesudah', $event)"
                  multiple
                  class="hidden"
                  ref="fotoSesudahInput"
              />
              <button
                  @click="fotoSesudahInput.click()"
                  :class="[
                    'w-full aspect-square border-2 border-dashed rounded-lg transition-all flex flex-col items-center justify-center bg-slate-50',
                    draggedOver === 'fotoSesudah' ? 'border-blue-500 bg-blue-50' : 'border-slate-300 hover:border-blue-500 hover:bg-blue-50'
                  ]"
              >
                <svg class="w-10 h-10 text-slate-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-slate-500 font-medium">Upload</span>
              </button>
              <div v-if="currentEntry.fotoSesudah.length > 0" class="mt-4 grid grid-cols-2 sm:grid-cols-3 gap-2">
                <div v-for="(image, index) in currentEntry.fotoSesudah" :key="`foto-sesudah-${index}`" class="relative aspect-square rounded-lg overflow-hidden border border-slate-200 group cursor-move">
                  <img
                      :src="image"
                      class="w-full h-full object-cover"
                      alt="Foto Sesudah"
                      draggable="true"
                      @dragstart="startPhotoDrag('fotoSesudah', index, $event)"
                  />
                  <button
                      @click="removeImage('fotoSesudah', index)"
                      class="absolute top-1 right-1 bg-red-500 text-white p-1 rounded-full hover:bg-red-600 transition-colors opacity-0 group-hover:opacity-100"
                      type="button"
                  >
                    <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Added Uraian Kegiatan checkbox section -->
        <div class="mb-6">
          <div class="flex items-center justify-between mb-3">
            <label class="block text-sm font-semibold text-slate-700">
              Uraian Kegiatan
            </label>
            <button
                @click="toggleAllActivities"
                class="text-sm text-blue-600 hover:text-blue-700 font-medium flex items-center gap-1"
            >
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              {{ allActivitiesSelected ? 'Uncheck All' : 'Check All' }}
            </button>
          </div>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3">
            <label
                v-for="activity in cleaningActivities"
                :key="activity"
                class="flex items-center gap-3 p-3 border border-slate-200 rounded-lg hover:bg-blue-50 cursor-pointer transition-colors"
            >
              <input
                  type="checkbox"
                  :value="activity"
                  v-model="currentEntry.activities"
                  class="w-5 h-5 text-blue-600 border-slate-300 rounded focus:ring-blue-500"
              />
              <span class="text-sm text-slate-700">{{ activity }}</span>
            </label>
          </div>
        </div>

        <button
            @click="addEntry"
            :disabled="!currentEntry.lokasi"
            class="w-full bg-blue-600 text-white py-4 rounded-lg hover:bg-blue-700 disabled:bg-slate-300 disabled:cursor-not-allowed transition-all font-semibold text-lg flex items-center justify-center gap-2 shadow-lg shadow-blue-600/30 hover:shadow-xl"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
          </svg>
          Tambah ke Daftar
        </button>
      </div>

      <!-- Updated entries list display -->
      <div class="bg-white rounded-xl shadow-md p-8 mb-6" v-if="entries.length > 0">
        <div class="flex flex-wrap items-center justify-between gap-4 mb-6">
          <div>
            <h2 class="text-2xl font-bold text-slate-900 flex items-center gap-2">
              <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
              Data Service
            </h2>
            <p class="text-slate-600 mt-1">Total: {{ entries.length }} entries ({{ Math.ceil(entries.length / 7) }} halaman)</p>
          </div>

          <div class="flex gap-3">
            <button
                @click="exportToExcel"
                class="bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition-all font-semibold flex items-center gap-2 shadow-lg shadow-green-600/30"
            >
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
              Export Excel
            </button>

            <button
                @click="generatePDF"
                class="bg-red-600 text-white px-6 py-3 rounded-lg hover:bg-red-700 transition-all font-semibold flex items-center gap-2 shadow-lg shadow-red-600/30"
            >
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2-2v14a2 2 0 002 2z" />
              </svg>
              Export PDF
            </button>
          </div>
        </div>

        <div class="space-y-4">
          <div
              v-for="(entry, index) in entries"
              :key="entry.id"
              class="border-2 border-slate-200 rounded-lg p-5 hover:shadow-lg hover:border-blue-300 transition-all"
          >
            <div class="flex justify-between items-start mb-4">
              <div>
                <h3 class="font-bold text-lg text-slate-900">{{ index + 1 }}. {{ entry.lokasi }}</h3>
                <p class="text-sm text-slate-500 mt-1">{{ entry.activities.length }} kegiatan dipilih</p>
              </div>
              <button
                  @click="deleteEntry(entry.id)"
                  class="text-red-600 hover:text-red-800 p-2 hover:bg-red-50 rounded-lg transition-colors"
              >
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                </svg>
              </button>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div v-if="entry.fotoLokasi && Array.isArray(entry.fotoLokasi) && entry.fotoLokasi.length > 0">
                <p class="text-xs font-semibold text-slate-600 mb-2">Lokasi</p>
                <!-- Fixed: Proper grid layout with smaller gap for preview -->
                <div class="grid grid-cols-2 gap-1">
                  <div v-for="(image, index) in entry.fotoLokasi" :key="index" class="aspect-square rounded-lg overflow-hidden border border-slate-200">
                    <img :src="image" class="w-full h-full object-cover" alt="Lokasi" />
                  </div>
                </div>
              </div>
              <div v-if="entry.fotoProses && Array.isArray(entry.fotoProses) && entry.fotoProses.length > 0">
                <p class="text-xs font-semibold text-slate-600 mb-2">Proses</p>
                <!-- Fixed: Proper grid layout with smaller gap for preview -->
                <div class="grid grid-cols-2 gap-1">
                  <div v-for="(image, index) in entry.fotoProses" :key="index" class="aspect-square rounded-lg overflow-hidden border border-slate-200">
                    <img :src="image" class="w-full h-full object-cover" alt="Proses" />
                  </div>
                </div>
              </div>
              <div v-if="entry.fotoSebelum && Array.isArray(entry.fotoSebelum) && entry.fotoSebelum.length > 0">
                <p class="text-xs font-semibold text-slate-600 mb-2">Sebelum</p>
                <!-- Fixed: Proper grid layout with smaller gap for preview -->
                <div class="grid grid-cols-2 gap-1">
                  <div v-for="(image, index) in entry.fotoSebelum" :key="index" class="aspect-square rounded-lg overflow-hidden border border-slate-200">
                    <img :src="image" class="w-full h-full object-cover" alt="Sebelum" />
                  </div>
                </div>
              </div>
              <div v-if="entry.fotoSesudah && Array.isArray(entry.fotoSesudah) && entry.fotoSesudah.length > 0">
                <p class="text-xs font-semibold text-slate-600 mb-2">Sesudah</p>
                <!-- Fixed: Proper grid layout with smaller gap for preview -->
                <div class="grid grid-cols-2 gap-1">
                  <div v-for="(image, index) in entry.fotoSesudah" :key="index" class="aspect-square rounded-lg overflow-hidden border border-slate-200">
                    <img :src="image" class="w-full h-full object-cover" alt="Sesudah" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Empty State -->
      <div v-else class="bg-white rounded-xl shadow-md p-12 text-center">
        <div class="inline-flex items-center justify-center w-20 h-20 bg-slate-100 rounded-full mb-4">
          <svg class="w-10 h-10 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
        </div>
        <h3 class="text-xl font-semibold text-slate-900 mb-2">Belum Ada Data</h3>
        <p class="text-slate-600">Mulai tambahkan data service AC di form di atas</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const buildingName = ref('');
const period = ref('September 2025');
const entries = ref([]);
const draggedOver = ref(null);
const dragSource = ref(null);
const currentEntry = ref({
  lokasi: '',
  fotoLokasi: [],
  fotoProses: [],
  fotoSebelum: [],
  fotoSesudah: [],
  activities: []
});

const cleaningActivities = [
  'Cleaning Evaporator',
  'Cleaning Filter Udara',
  'Cleaning Bak Drain',
  'Cleaning Jalur Drain',
  'Cleaning Boddy Unit'
];

const dynamicTitle = computed(() => {
  if (currentEntry.value.activities.length === 0) {
    return 'FOTO DOKUMENTASI SERVICE';
  }

  // Map activities to their AC types
  const acTypes = new Set();
  const typeMap = {
    'Cassette': 'AC CASSETTE',
    'Split Wall': 'AC SPLIT WALL',
    'AHU': 'AC AHU',
    'Evaporator': 'AC EVAPORATOR',
    'Filter Udara': 'AC FILTER UDARA',
    'Drain': 'AC DRAIN'
  };

  currentEntry.value.activities.forEach(activity => {
    // Check each activity against the type map
    Object.entries(typeMap).forEach(([key, type]) => {
      if (activity.includes(key)) {
        acTypes.add(type);
      }
    });
  });

  if (acTypes.size === 0) {
    return 'FOTO DOKUMENTASI SERVICE';
  }

  const typesList = Array.from(acTypes);
  const titleSuffix = typesList.join(' & ');
  return `FOTO DOKUMENTASI SERVICE ${titleSuffix}`;
});

const allPhotosSelected = computed(() => {
  return !!(currentEntry.value.fotoLokasi.length > 0 &&
      currentEntry.value.fotoProses.length > 0 &&
      currentEntry.value.fotoSebelum.length > 0 &&
      currentEntry.value.fotoSesudah.length > 0);
});

const allActivitiesSelected = computed(() => {
  return currentEntry.value.activities.length === cleaningActivities.length;
});

const resizeImageToSquare = (file) => {
  return new Promise((resolve) => {
    const reader = new FileReader();
    reader.onload = (e) => {
      const img = new Image();
      img.onload = () => {
        const canvas = document.createElement('canvas');
        const size = Math.min(img.width, img.height);
        canvas.width = 800;
        canvas.height = 800;

        const ctx = canvas.getContext('2d');
        const offsetX = (img.width - size) / 2;
        const offsetY = (img.height - size) / 2;

        ctx.drawImage(img, offsetX, offsetY, size, size, 0, 0, 800, 800);
        resolve(canvas.toDataURL('image/jpeg', 0.9));
      };
      img.src = e.target.result;
    };
    reader.readAsDataURL(file);
  });
};

const handleImageUpload = async (field, event) => {
  const files = event.target.files;
  if (files && files.length > 0) {
    const uploadedImages = [];

    for (let i = 0; i < files.length; i++) {
      const file = files[i];
      if (file.type.startsWith('image/')) {
        const resizedImage = await resizeImageToSquare(file);
        uploadedImages.push(resizedImage);
      }
    }

    if (!Array.isArray(currentEntry.value[field])) {
      currentEntry.value[field] = [];
    }
    currentEntry.value[field].push(...uploadedImages);
  }
};

const startPhotoDrag = (field, index, event) => {
  dragSource.value = { field, index };
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('application/json', JSON.stringify({
    source: field,
    index: index,
    imageData: currentEntry.value[field][index]
  }));
};

const handlePhotoDrop = async (field, event) => {
  if (dragSource.value) {
    // If dragging from one field to another
    const sourceField = dragSource.value.field;
    const sourceIndex = dragSource.value.index;
    
    if (sourceField === field) {
      // If dropping on the same field, do nothing
      dragSource.value = null;
      draggedOver.value = null;
      return;
    }

    if (Array.isArray(currentEntry.value[sourceField]) && currentEntry.value[sourceField][sourceIndex]) {
      const sourceImage = currentEntry.value[sourceField][sourceIndex];
      const targetImage = currentEntry.value[field]?.[0] || null;
      
      // Swap the images
      if (targetImage) {
        // If target has an image, swap them
        currentEntry.value[sourceField][sourceIndex] = targetImage;
      } else {
        // If target is empty, just move the image
        currentEntry.value[sourceField].splice(sourceIndex, 1);
      }
      
      // Set the target field with the source image
      currentEntry.value[field] = [sourceImage];
    }
  } else if (event.dataTransfer.files.length > 0) {
    // Handle file drop from outside
    const file = event.dataTransfer.files[0];
    if (file?.type.startsWith('image/')) {
      const resizedImage = await resizeImageToSquare(file);
      currentEntry.value[field] = [resizedImage];
    }
  }
  
  dragSource.value = null;
  draggedOver.value = null;
};

const removeImage = (field, index) => {
  if (index !== undefined) {
    currentEntry.value[field].splice(index, 1);
  } else {
    currentEntry.value[field] = null;
  }
};

const selectAllPhotos = async () => {
  if (allPhotosSelected.value) {
    resetCurrentEntry();
    return;
  }
  
  try {
    // Create a file input element
    const input = document.createElement('input');
    input.type = 'file';
    input.multiple = true;
    input.accept = 'image/*';
    
    // Handle file selection
    input.onchange = async (e) => {
      const files = Array.from(e.target.files);
      const imageFields = ['fotoLokasi', 'fotoProses', 'fotoSebelum', 'fotoSesudah'];
      
      // Clear all photo fields first
      imageFields.forEach(field => {
        currentEntry.value[field] = [];
      });
      
      // Process up to 4 images
      const maxImages = Math.min(files.length, 4);
      for (let i = 0; i < maxImages; i++) {
        const file = files[i];
        if (file.type.startsWith('image/')) {
          const resizedImage = await resizeImageToSquare(file);
          currentEntry.value[imageFields[i]] = [resizedImage];
        }
      }
    };
    
    // Trigger file dialog
    input.click();
  } catch (error) {
    console.error('Error selecting photos:', error);
  }
};

const toggleAllActivities = () => {
  if (allActivitiesSelected.value) {
    currentEntry.value.activities = [];
  } else {
    currentEntry.value.activities = [...cleaningActivities];
  }
};

const addEntry = () => {
  if (currentEntry.value.lokasi) {
    entries.value.push({
      ...currentEntry.value,
      id: Date.now(),
      activities: [...currentEntry.value.activities]
    });

    resetCurrentEntry();
  }
};

const deleteEntry = (id) => {
  entries.value = entries.value.filter(entry => entry.id !== id);
};

const generatePDF = () => {
  const pages = [];
  for (let i = 0; i < entries.value.length; i += 7) {
    pages.push(entries.value.slice(i, i + 7));
  }

  let printContent = `
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="UTF-8">
      <style>
        @page {
          size: A4 portrait;
          margin: 15mm;
        }
        * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
        }
        body {
          font-family: Arial, sans-serif;
          font-size: 9px;
        }
        .page {
          page-break-after: always;
          width: 100%;
        }
        .page:last-child {
          page-break-after: auto;
        }
        .header {
          text-align: center;
          margin-bottom: 10px;
          border-bottom: 2px solid #000;
          padding-bottom: 8px;
        }
        .header h2 {
          margin: 2px 0;
          font-size: 13px;
          font-weight: bold;
        }
        .header p {
          margin: 2px 0;
          font-size: 10px;
        }
        table {
          width: 100%;
          border-collapse: collapse;
          margin-top: 8px;
        }
        th, td {
          border: 1px solid #000;
          padding: 4px;
          vertical-align: top;
        }
        th {
          background-color: #d0d0d0;
          font-weight: bold;
          text-align: center;
          font-size: 10px;
        }
        .no-col { width: 5%; text-align: center; font-weight: bold; }
        .lokasi-col { width: 19%; text-align: center; }
        .proses-col { width: 19%; text-align: center; }
        .sebelum-col { width: 19%; text-align: center; }
        .sesudah-col { width: 19%; text-align: center; }
        .kegiatan-col { width: 19%; }
        .foto-img {
          width: 100%;
          height: 100px;
          object-fit: cover;
          display: block;
        }
        .kegiatan-list {
          list-style: none;
          padding-left: 0;
          font-size: 8px;
          line-height: 1.4;
        }
        .kegiatan-list li {
          margin: 1px 0;
        }
        .kegiatan-list li:before {
          content: "> ";
          font-weight: bold;
        }
        .cell-label {
          font-size: 8px;
          font-weight: bold;
          margin-bottom: 3px;
          text-align: center;
        }
      </style>
    </head>
    <body>
  `;

  pages.forEach((pageEntries) => {
    printContent += `
      <div class="page">
        <div class="header">
          <h2>FOTO DOKUMENTASI SERVICE AC NON VRV</h2>
          <h2>${buildingName.value}</h2>
          <p>Periode : ${period.value}</p>
        </div>

        <table>
          <thead>
            <tr>
              <th class="no-col">NO</th>
              <th class="lokasi-col">LOKASI</th>
              <th class="proses-col">PROSES</th>
              <th class="sebelum-col">SEBELUM</th>
              <th class="sesudah-col">SESUDAH</th>
              <th class="kegiatan-col">URAIAN KEGIATAN</th>
            </tr>
          </thead>
          <tbody>
    `;

    pageEntries.forEach((entry, index) => {
      printContent += `
        <tr>
          <td class="no-col">${entries.value.indexOf(entry) + 1}</td>
          <td class="lokasi-col">
            ${entry.fotoLokasi.length > 0 ? entry.fotoLokasi.map(image => `<img src="${image}" class="foto-img" alt="Lokasi" />`).join('') : ''}
          </td>
          <td class="proses-col">
            ${entry.fotoProses.length > 0 ? entry.fotoProses.map(image => `<img src="${image}" class="foto-img" alt="Proses" />`).join('') : ''}
          </td>
          <td class="sebelum-col">
            ${entry.fotoSebelum.length > 0 ? entry.fotoSebelum.map(image => `<img src="${image}" class="foto-img" alt="Sebelum" />`).join('') : ''}
          </td>
          <td class="sesudah-col">
            ${entry.fotoSesudah.length > 0 ? entry.fotoSesudah.map(image => `<img src="${image}" class="foto-img" alt="Sesudah" />`).join('') : ''}
          </td>
          <td class="kegiatan-col">
            <div class="cell-label">${entry.lokasi}</div>
            <ul class="kegiatan-list">
              ${entry.activities.map(activity => `<li>${activity}</li>`).join('')}
            </ul>
          </td>
        </tr>
      `;
    });

    printContent += `
          </tbody>
        </table>
      </div>
    `;
  });

  printContent += `
    </body>
    </html>
  `;

  const printWindow = window.open('', '_blank');
  printWindow.document.write(printContent);
  printWindow.document.close();

  setTimeout(() => {
    printWindow.print();
  }, 500);
};

const exportToExcel = () => {
  let csvContent = "data:text/csv;charset=utf-8,";
  csvContent += "No,Lokasi,Uraian Kegiatan,Foto Lokasi,Foto Proses,Foto Sebelum,Foto Sesudah\n";

  entries.value.forEach((entry, index) => {
    const activities = entry.activities.join('; ');
    const fotoLokasi = entry.fotoLokasi.length > 0 ? 'Yes' : 'No';
    const fotoProses = entry.fotoProses.length > 0 ? 'Yes' : 'No';
    const fotoSebelum = entry.fotoSebelum.length > 0 ? 'Yes' : 'No';
    const fotoSesudah = entry.fotoSesudah.length > 0 ? 'Yes' : 'No';
    csvContent += `${index + 1},"${entry.lokasi}","${activities}",${fotoLokasi},${fotoProses},${fotoSebelum},${fotoSesudah}\n`;
  });

  const encodedUri = encodeURI(csvContent);
  const link = document.createElement("a");
  link.setAttribute("href", encodedUri);
  link.setAttribute("download", `${buildingName.value}_${period.value}.csv`);
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
};

const fotoLokasiInput = ref(null);
const fotoProsesInput = ref(null);
const fotoSebelumInput = ref(null);
const fotoSesudahInput = ref(null);

const resetCurrentEntry = () => {
  currentEntry.value = {
    lokasi: '',
    fotoLokasi: [],
    fotoProses: [],
    fotoSebelum: [],
    fotoSesudah: [],
    activities: []
  };
};
</script>
