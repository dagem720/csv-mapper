<template>
  <div class="w-full">
    <div class="w-full md:flex md:items-center md:justify-between">
      <div class="min-w-0">
        <h2
          class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate"
        >
          CSV Mapper
        </h2>
      </div>
      <div class="flex mt-4 md:mt-0 md:ml-4">
        <button
          @click="isOpen = true"
          type="button"
          class="inline-flex items-center px-4 py-2 ml-3 text-sm font-medium text-white bg-indigo-600 border border-transparent rounded-md shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
        >
          Upload File
        </button>
      </div>
    </div>
    <div class="flex flex-col mt-8">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle md:px-6 lg:px-8">
          <div
            class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 md:rounded-lg"
          >
            <div
              v-if="dataList.length === 0"
              class="flex items-center justify-center w-full h-96"
            >
              <p class="text-sm text-gray-500 dark:text-gray-400">
                No data to display
              </p>
            </div>
            <table class="min-w-full divide-y divide-gray-300">
              <thead class="bg-gray-50">
                <tr>
                  <th
                    v-for="(header, i) in headerList"
                    :key="i"
                    class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
                  >
                    {{ header }}
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(data, i) in dataList" :key="i">
                  <td
                    v-for="(value, key) in data"
                    :key="key"
                    class="py-4 pl-4 pr-3 text-sm font-medium text-gray-900 whitespace-nowrap sm:pl-6"
                  >
                    {{ value }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

  <uploadFileModal :mapCsv="mapCsv" :isOpen="isOpen" :closeModal="closeModal" />
</template>

<script setup lang="ts">
import { ref } from "vue";
import uploadFileModal from "./uploadFileModal.vue";

const isOpen = ref(false);
const closeModal = () => {
  isOpen.value = false;
};

const dataList = ref<any>([]);
const headerList = ref<any>([]);

const mapCsv = (data: { file: File }) => {
  const { file } = data;
  const reader = new FileReader();
  reader.onload = () => {
    const results = reader.result;
    const fileContent = results?.toString();
    const rows = fileContent?.split("\n");
    if (rows) {
      const headers = rows[0].split(",");
      headers.forEach((header) => {
        headerList.value.push(header);
      });
      const values = rows.slice(1);
      const mappedValues = values.map((value) => {
        const obj = {};
        const valueArray = value.split(",");
        headers.forEach((header, index) => {
          obj[header] = valueArray[index];
        });
        return obj;
      });
      dataList.value = mappedValues;
    }
  };
  reader.readAsText(file);
};
</script>

<style scoped></style>
