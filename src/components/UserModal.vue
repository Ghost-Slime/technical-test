<template>
    <div class="fixed inset-0 bg-gray-600 bg-opacity-50 flex justify-center items-center">
      <div class="bg-white p-6 rounded-lg shadow-lg max-w-md w-full">
        <h2 class="text-xl font-bold mb-4">
          {{ user.name.first }} {{ user.name.last }}
        </h2>
        <img
          :src="user.picture.large"
          :alt="`${user.name.first} ${user.name.last}`"
          class="rounded-full mx-auto mb-4"
        />
        <p><strong>Email:</strong> {{ user.email }}</p>
        <p><strong>Phone:</strong> {{ user.phone }}</p>
        <p><strong>Location:</strong> {{ user.location.city }}, {{ user.location.country }}</p>
        <button
          @click="$emit('close')"
          class="mt-4 px-4 py-2 bg-red-500 text-white rounded w-full"
        >
          Close
        </button>
      </div>
    </div>
  </template>

<script setup lang="ts">
defineProps({ user: Object });
defineEmits(["close"]);
</script>