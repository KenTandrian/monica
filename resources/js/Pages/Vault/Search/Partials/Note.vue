<script setup>
import { ref } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
  data: Object,
});

const localNotes = ref(props.data);

const showFull = (note) => {
  localNotes.value[localNotes.value.findIndex((x) => x.id === note.id)].show_full_content = true;
};
</script>

<template>
  <div>
    <div class="mb-2 sm:mb-1">
      <span class="relative">
        <svg
          class="icon-sidebar relative inline h-4 w-4"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg">
          <path
            d="M6 6C6 5.44772 6.44772 5 7 5H17C17.5523 5 18 5.44772 18 6C18 6.55228 17.5523 7 17 7H7C6.44771 7 6 6.55228 6 6Z"
            fill="currentColor" />
          <path
            d="M6 10C6 9.44771 6.44772 9 7 9H17C17.5523 9 18 9.44771 18 10C18 10.5523 17.5523 11 17 11H7C6.44771 11 6 10.5523 6 10Z"
            fill="currentColor" />
          <path
            d="M7 13C6.44772 13 6 13.4477 6 14C6 14.5523 6.44771 15 7 15H17C17.5523 15 18 14.5523 18 14C18 13.4477 17.5523 13 17 13H7Z"
            fill="currentColor" />
          <path
            d="M6 18C6 17.4477 6.44772 17 7 17H11C11.5523 17 12 17.4477 12 18C12 18.5523 11.5523 19 11 19H7C6.44772 19 6 18.5523 6 18Z"
            fill="currentColor" />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M2 4C2 2.34315 3.34315 1 5 1H19C20.6569 1 22 2.34315 22 4V20C22 21.6569 20.6569 23 19 23H5C3.34315 23 2 21.6569 2 20V4ZM5 3H19C19.5523 3 20 3.44771 20 4V20C20 20.5523 19.5523 21 19 21H5C4.44772 21 4 20.5523 4 20V4C4 3.44772 4.44771 3 5 3Z"
            fill="currentColor" />
        </svg>
      </span>

      {{ $t('Notes') }}
    </div>
    <ul v-if="localNotes.length > 0">
      <li
        v-for="note in localNotes"
        :key="note.id"
        class="mb-4 rounded-xs border border-gray-200 last:mb-0 dark:border-gray-700">
        <div
          v-if="note.title"
          class="mb-1 border-b border-gray-200 p-3 text-xs font-semibold text-gray-600 dark:border-gray-700 dark:text-gray-400">
          {{ note.title }}
        </div>
        <div v-if="!note.show_full_content" class="p-3">
          {{ note.body_excerpt }}
          <span class="cursor-pointer text-blue-500 hover:underline" @click="showFull(note)">{{ $t('View all') }}</span>
        </div>
        <div v-else class="p-3">
          {{ note.body }}
        </div>
        <div
          class="flex border-t border-gray-200 px-3 py-2 text-xs text-gray-600 hover:rounded-b hover:bg-slate-50 dark:border-gray-700 dark:bg-slate-900 dark:text-gray-400 dark:hover:bg-slate-800">
          <!-- date -->
          <div class="relative me-3 inline">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="icon-note relative inline h-4 w-4 text-gray-400"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            {{ note.written_at }}
          </div>

          <!-- contact -->
          <div class="relative me-3 inline">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="icon-note relative me-1 inline h-4 w-4 text-gray-400"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5.121 17.804A13.937 13.937 0 0112 16c2.5 0 4.847.655 6.879 1.804M15 10a3 3 0 11-6 0 3 3 0 016 0zm6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <Link :href="note.contact.url" class="text-blue-500 hover:underline">
              {{ note.contact.name }}
            </Link>
          </div>
        </div>
      </li>
    </ul>
    <!-- blank state -->
    <div
      v-else
      class="mb-6 rounded-lg border border-gray-200 bg-white p-5 text-center text-gray-500 dark:border-gray-700 dark:bg-gray-900">
      {{ $t('No notes found.') }}
    </div>
  </div>
</template>

<style lang="scss" scoped>
.icon-sidebar {
  color: #737e8d;
  top: -2px;
}

.icon-note {
  top: -1px;
}
</style>
