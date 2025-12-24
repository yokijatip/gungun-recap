<template>
  <div class="min-h-screen bg-gray-50 p-6">
    <div class="max-w-7xl mx-auto">
      <!-- Header -->
      <div class="bg-white rounded-lg shadow-md p-6 mb-6">
        <h1 class="text-2xl font-bold text-gray-800 mb-2">
          Generator Laporan Service AC
        </h1>
        <p class="text-gray-600">
          FOTO DOKUMENTASI SERVICE AC NON VRV - KANTOR GEDUNG DITJEN IMIGRASI
        </p>

        <!-- Period Input -->
        <div class="mt-4">
          <label class="block text-sm font-medium text-gray-700 mb-2">
            Periode
          </label>
          <input
              v-model="period"
              type="text"
              class="px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              placeholder="Contoh: September 2025"
          />
        </div>
      </div>

      <!-- Form Input Entry -->
      <div class="bg-white rounded-lg shadow-md p-6 mb-6">
        <h2 class="text-xl font-semibold text-gray-800 mb-4">
          Tambah Data Service
        </h2>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Nomor
            </label>
            <input
                v-model="currentEntry.no"
                type="number"
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                placeholder="No urut"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Lokasi
            </label>
            <input
                v-model="currentEntry.lokasi"
                type="text"
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                placeholder="Nama lokasi"
            />
          </div>
        </div>

        <!-- Upload Foto -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Foto Lokasi
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoLokasi', $event)"
                  class="hidden"
                  ref="fotoLokasiInput"
              />
              <button
                  @click="$refs.fotoLokasiInput.click()"
                  class="w-full px-4 py-8 border-2 border-dashed border-gray-300 rounded-lg hover:border-blue-500 transition-colors flex flex-col items-center justify-center"
              >
                <svg class="w-8 h-8 text-gray-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-gray-500">Upload Foto</span>
              </button>
              <img
                  v-if="currentEntry.fotoLokasi"
                  :src="currentEntry.fotoLokasi"
                  class="mt-2 w-full h-32 object-cover rounded-lg"
                  alt="Preview Lokasi"
              />
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Foto Sebelum
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoSebelum', $event)"
                  class="hidden"
                  ref="fotoSebelumInput"
              />
              <button
                  @click="$refs.fotoSebelumInput.click()"
                  class="w-full px-4 py-8 border-2 border-dashed border-gray-300 rounded-lg hover:border-blue-500 transition-colors flex flex-col items-center justify-center"
              >
                <svg class="w-8 h-8 text-gray-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-gray-500">Upload Foto</span>
              </button>
              <img
                  v-if="currentEntry.fotoSebelum"
                  :src="currentEntry.fotoSebelum"
                  class="mt-2 w-full h-32 object-cover rounded-lg"
                  alt="Preview Sebelum"
              />
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Foto Sesudah
            </label>
            <div class="relative">
              <input
                  type="file"
                  accept="image/*"
                  @change="handleImageUpload('fotoSesudah', $event)"
                  class="hidden"
                  ref="fotoSesudahInput"
              />
              <button
                  @click="$refs.fotoSesudahInput.click()"
                  class="w-full px-4 py-8 border-2 border-dashed border-gray-300 rounded-lg hover:border-blue-500 transition-colors flex flex-col items-center justify-center"
              >
                <svg class="w-8 h-8 text-gray-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                </svg>
                <span class="text-sm text-gray-500">Upload Foto</span>
              </button>
              <img
                  v-if="currentEntry.fotoSesudah"
                  :src="currentEntry.fotoSesudah"
                  class="mt-2 w-full h-32 object-cover rounded-lg"
                  alt="Preview Sesudah"
              />
            </div>
          </div>
        </div>

        <button
            @click="addEntry"
            :disabled="!currentEntry.lokasi"
            class="w-full bg-blue-600 text-white py-3 rounded-lg hover:bg-blue-700 disabled:bg-gray-300 disabled:cursor-not-allowed transition-colors font-medium flex items-center justify-center gap-2"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
          </svg>
          Tambah Data
        </button>
      </div>

      <!-- List Entries -->
      <div class="bg-white rounded-lg shadow-md p-6 mb-6" v-if="entries.length > 0">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl font-semibold text-gray-800">
            Data Service ({{ entries.length }} entries)
          </h2>
          <button
              @click="generatePDF"
              class="bg-green-600 text-white px-6 py-2 rounded-lg hover:bg-green-700 transition-colors font-medium flex items-center gap-2"
          >
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
            Export ke PDF
          </button>
        </div>

        <div class="space-y-4">
          <div
              v-for="entry in entries"
              :key="entry.id"
              class="border border-gray-200 rounded-lg p-4 hover:shadow-md transition-shadow"
          >
            <div class="flex justify-between items-start mb-3">
              <div>
                <h3 class="font-semibold text-gray-800">{{ entry.no }}. {{ entry.lokasi }}</h3>
              </div>
              <button
                  @click="deleteEntry(entry.id)"
                  class="text-red-600 hover:text-red-800 p-2 hover:bg-red-50 rounded transition-colors"
              >
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                </svg>
              </button>
            </div>

            <div class="grid grid-cols-3 gap-4">
              <div v-if="entry.fotoLokasi">
                <p class="text-xs text-gray-600 mb-1">Lokasi</p>
                <img :src="entry.fotoLokasi" class="w-full h-24 object-cover rounded" alt="Lokasi" />
              </div>
              <div v-if="entry.fotoSebelum">
                <p class="text-xs text-gray-600 mb-1">Sebelum</p>
                <img :src="entry.fotoSebelum" class="w-full h-24 object-cover rounded" alt="Sebelum" />
              </div>
              <div v-if="entry.fotoSesudah">
                <p class="text-xs text-gray-600 mb-1">Sesudah</p>
                <img :src="entry.fotoSesudah" class="w-full h-24 object-cover rounded" alt="Sesudah" />
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Preview Area (Hidden, for PDF generation) -->
      <div id="printArea" class="hidden"></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const entries = ref([]);
const period = ref('September 2025');
const currentEntry = ref({
  no: '',
  lokasi: '',
  fotoLokasi: null,
  fotoSebelum: null,
  fotoSesudah: null
});

const cleaningActivities = [
  'Cleaning Evaporator',
  'Cleaning Filter Udara',
  'Cleaning Bak Drain',
  'Cleaning Pompa Drain',
  'Cleaning Jalur Drain',
  'Cleaning Boddy Unit'
];

const handleImageUpload = (field, event) => {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      currentEntry.value[field] = e.target.result;
    };
    reader.readAsDataURL(file);
  }
};

const addEntry = () => {
  if (currentEntry.value.lokasi) {
    entries.value.push({
      ...currentEntry.value,
      id: Date.now()
    });

    // Reset form
    currentEntry.value = {
      no: '',
      lokasi: '',
      fotoLokasi: null,
      fotoSebelum: null,
      fotoSesudah: null
    };
  }
};

const deleteEntry = (id) => {
  entries.value = entries.value.filter(entry => entry.id !== id);
};

const generatePDF = () => {
  // Split entries into pages (7 per page)
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
          size: A4 landscape;
          margin: 15mm;
        }
        * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
        }
        body {
          font-family: Arial, sans-serif;
          font-size: 10px;
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
        }
        .header h2 {
          margin: 3px 0;
          font-size: 14px;
        }
        .header p {
          margin: 2px 0;
          font-size: 11px;
        }
        table {
          width: 100%;
          border-collapse: collapse;
          margin-top: 5px;
        }
        th, td {
          border: 1px solid #000;
          padding: 5px;
          vertical-align: top;
        }
        th {
          background-color: #e0e0e0;
          font-weight: bold;
          text-align: center;
          font-size: 11px;
        }
        .no-col { width: 5%; text-align: center; }
        .lokasi-col { width: 20%; }
        .proses-col { width: 25%; }
        .foto-col { width: 25%; text-align: center; }
        .foto-img {
          max-width: 100%;
          max-height: 120px;
          object-fit: contain;
        }
        .proses-list {
          list-style: none;
          padding-left: 0;
          font-size: 9px;
        }
        .proses-list li {
          margin: 2px 0;
        }
        .proses-list li:before {
          content: "> ";
        }
      </style>
    </head>
    <body>
  `;

  pages.forEach((pageEntries, pageIndex) => {
    printContent += `
      <div class="page">
        <div class="header">
          <h2>FOTO DOKUMENTASI SERVICE AC NON VRV</h2>
          <h2>KANTOR GEDUNG DITJEN IMIGRASI</h2>
          <p>Periode : ${period.value}</p>
        </div>

        <table>
          <thead>
            <tr>
              <th class="no-col">NO</th>
              <th class="lokasi-col">LOKASI</th>
              <th class="proses-col">PROSES</th>
              <th class="foto-col">SEBELUM</th>
              <th class="foto-col">SESUDAH</th>
            </tr>
          </thead>
          <tbody>
    `;

    pageEntries.forEach(entry => {
      printContent += `
        <tr>
          <td class="no-col">${entry.no}</td>
          <td class="lokasi-col">
            ${entry.fotoLokasi ? `<img src="${entry.fotoLokasi}" class="foto-img" alt="Lokasi" />` : ''}
          </td>
          <td class="proses-col">
            <ul class="proses-list">
              ${cleaningActivities.map(activity => `<li>${activity}</li>`).join('')}
            </ul>
          </td>
          <td class="foto-col">
            ${entry.fotoSebelum ? `<img src="${entry.fotoSebelum}" class="foto-img" alt="Sebelum" />` : ''}
          </td>
          <td class="foto-col">
            ${entry.fotoSesudah ? `<img src="${entry.fotoSesudah}" class="foto-img" alt="Sesudah" />` : ''}
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

  // Open print window
  const printWindow = window.open('', '_blank');
  printWindow.document.write(printContent);
  printWindow.document.close();

  // Wait for images to load before printing
  setTimeout(() => {
    printWindow.print();
  }, 500);
};
</script>