<template>
  <div v-if="isOpen">
    <div class="fixed inset-0 z-50 flex items-center justify-center">
      <div class="fixed inset-0 bg-black opacity-50"></div>
      <div
        class="fixed top-0 bottom-0 left-0 right-0 flex items-center justify-center"
      >
        <div
          class="bg-white w-full mx-5 md:mx-0 md:w-[50%] p-6 flex flex-col space-y-4 rounded-lg shadow-lg relative"
        >
          <button
            @click="onClose"
            class="absolute p-2 top-0 right-0 m-4 text-gray-500 border border-gray-500 !bg-white hover:text-gray-800"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-6 h-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="{2}"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>

          <h2
            class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate"
          >
            CSV Mapper
          </h2>

          <div class="flex items-center justify-center w-full">
            <label
              for="dropzone-file"
              class="flex flex-col items-center justify-center w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer"
            >
              <div
                class="flex flex-col items-center justify-center pt-5 pb-6"
                @dragover.prevent
                @dragenter.prevent
                @dragleave.prevent
                @drop.prevent="dragOver"
              >
                <svg
                  class="w-8 h-8 mb-4 text-gray-500 dark:text-gray-400"
                  aria-hidden="true"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 20 16"
                >
                  <path
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M13 13h3a3 3 0 0 0 0-6h-.025A5.56 5.56 0 0 0 16 6.5 5.5 5.5 0 0 0 5.207 5.021C5.137 5.017 5.071 5 5 5a4 4 0 0 0 0 8h2.167M10 15V6m0 0L8 8m2-2 2 2"
                  />
                </svg>
                <p class="mb-2 text-sm text-gray-500 dark:text-gray-400">
                  <span class="font-semibold">Click to upload</span> or drag and
                  drop
                </p>
                <p class="text-xs text-gray-500 dark:text-gray-400">
                  SVG, PNG, JPG or GIF (MAX. 800x400px)
                </p>
              </div>
              <input
                @change="onFilePicked"
                id="dropzone-file"
                type="file"
                class="hidden"
              />
            </label>
          </div>
          <div class="" v-if="fileInput">
            <div>
              <p class="text-sm text-gray-500 dark:text-gray-400">
                {{ fileInput.name }}
              </p>
              <div class="flex justify-end mt-4 md:mt-0 md:ml-4">
                <button
                  @click="mapCsv"
                  type="button"
                  class="inline-flex items-center px-4 py-2 ml-3 text-sm font-medium text-white bg-indigo-600 border border-transparent rounded-md shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                >
                  Map CSV
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";
const props = defineProps<{
  closeModal: () => void;
  isOpen: boolean;
  mapCsv: (data: { file: File }) => void;
}>();

const fileInput = ref<File | null>(null);

const dragOver = (e: DragEvent) => {
  e.preventDefault();
  e.stopPropagation();
  fileInput.value = e.dataTransfer?.files[0] as File;
};

const onFilePicked = (e) => {
  fileInput.value = e.target.files[0];
};

const mapCsv = () => {
  if (fileInput.value) {
    props.closeModal();
    props.mapCsv({ file: fileInput.value });
  }
};

const onClose = () => {
  props.closeModal();
};
</script>

<style scoped></style>
