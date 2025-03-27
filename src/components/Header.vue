<template>
    <div class="flex justify-between items-center py-4 bg-white">
      <img src="@/assets/Logo.png" class="w-50"/>
      <div class="flex gap-4">
        <Bell class="text-black!" />
        <Settings class="text-black!" />
        <LogOut class="text-black!" />
      </div>
    </div>
  </template>

<script setup>
import { Bell, Settings, LogOut  } from 'lucide-vue-next';
</script>