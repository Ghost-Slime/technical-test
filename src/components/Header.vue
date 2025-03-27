<template>
    <div class="container mx-auto p-6 flex justify-between items-center">
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