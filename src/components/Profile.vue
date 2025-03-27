<template>
  <div class="bg-blue-400 text-white p-6 rounded-lg flex items-center gap-4">
    <Avatar :image="AvatarImage" size="xlarge" />
    <div class="flex">
      <div>
        <div class="text-4xl font-semibold mb-1">John Doe</div>
        <div class="text-sm text-gray-100">Last online: 2 days ago</div>
      </div>
      <div class="flex items-end ml-6">
        <div class="ml-auto flex gap-2">
          <Button label="Send Message" class="p-button-outlined bg-white! text-blue-400! hover:bg-blue-400! hover:text-white!">
            <template #icon>
              <Send :size="16" />
            </template>
          </Button>
          <Button label="Add Friend" class="p-button-outlined text-white! hover:bg-white! hover:text-blue-400!">
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
