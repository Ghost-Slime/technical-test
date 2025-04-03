<template>
  <div class="bg-blue-400 text-white w-full h-40">
    <div class="container flex items-end gap-4 mx-auto">
      <div class="mr-40">
        <div class="relative">
          <Avatar :image="AvatarImage" class="absolute -top-45 border-white shadow-lg custom-avatar" />
        </div>
      </div>
    <div class="flex pl-8 py-18">
      <div>
        <div class="text-4xl font-semibold mb-1">John Doe</div>
        <div class="text-sm text-gray-100">Last online: 2 days ago</div>
      </div>
    </div>
      <div class="flex py-18">
        <div class="ml-auto flex gap-2">
          <Button label="Send Message" class="p-button-outlined border-white! bg-white! text-blue-400! hover:bg-blue-400! hover:text-white!">
            <template #icon>
              <Send :size="16" />
            </template>
          </Button>
          <Button label="Add Friend" class="p-button-outlined border-white! text-white! hover:bg-white! hover:text-blue-400!">
            <template #icon>
              <Plus :size="16" />
            </template>
          </Button>
        </div>
      </div>
  </div>
  </div>
</template>

<script setup lang="ts">
import Avatar from "primevue/avatar";
import AvatarImage from "@/assets/Avatar.png";
import Button from "primevue/button";
import { Send, Plus } from "lucide-vue-next";
</script>

<style scoped>
.custom-avatar {
  width: 175px;  /* Adjust as needed */
  height: 175px;
  font-size: 24px; /* Adjust text size */
}
</style>
