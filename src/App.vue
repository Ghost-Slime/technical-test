<template>
  <div class="min-h-screen bg-white flex flex-col items-center">
    <!-- Header -->
    <div class="w-full">
      <Header />
    </div>

    <!-- Profile Section -->
    <div class="w-full mb-4">
      <Profile />
    </div>

    <main class="container mx-auto p-6">

      <!-- Users Section -->
      <div class="mt-6">
        <InputText
          v-model="searchQuery"
          placeholder="Search users by name"
          class="p-inputtext-sm w-full mb-3"
        />
        <DataTable
          :value="filteredUsers"
          paginator
          :rows="5"
          :rowsPerPageOptions="[5, 10, 20, 50]"
          class="custom-table cursor-pointer"
          @row-click="openModal"
        >
          <Column field="date" header="Date" class="bg-white! text-black!">
            <template #body="slotProps">
              <div>{{ convertDate(slotProps.data.dob.date) }}</div>
            </template>
          </Column>
          <Column field="name" header="Name" class="bg-white! text-black!">
            <template #body="slotProps">
              <div>
                <div>
                  {{ slotProps.data.name.first }} {{ slotProps.data.name.last }}
                </div>
              </div>
            </template>
          </Column>
          <Column field="gender" header="Gender" class="bg-white! text-black!">
            <template #body="slotProps">
              <div>{{ slotProps.data.gender.charAt(0).toUpperCase() + slotProps.data.gender.slice(1) }}</div>
            </template>
          </Column>
          <Column
            field="country"
            header="Country"
            class="bg-white! text-black!"
          >
            <template #body="slotProps">
              <div>{{ slotProps.data.location.country }}</div>
            </template>
          </Column>
          <Column field="email" header="Email" class="bg-white! text-black!">
            <template #body="slotProps">
              <div class="text-gray-500">{{ slotProps.data.email }}</div>
            </template>
          </Column>
        </DataTable>
        <div class="flex justify-center mt-4">
          <Button label="Refresh" class="border-0 bg-blue-400! text-white!" @click="fetchUsers">
            <template #icon>
              <RefreshCw  :size="16" />
            </template>
          </Button>
        </div>
      </div>

      <Dialog
        v-model:visible="selectedUser"
        modal
        :header="
          selectedUser
            ? `${selectedUser.name.first} ${selectedUser.name.last}`
            : ''
        "
        class="bg-white! text-black!"
        :style="{ width: '50vw' }"
        :breakpoints="{ '1199px': '75vw', '575px': '90vw' }"
      >
        <div v-if="selectedUser" class="w-1/2">
          <div class="grid grid-cols-2 gap-4 mb-4">
            <label class="font-medium pl-8">Date:</label>
            <p>{{ convertDate(selectedUser.dob.date) }}</p>
          </div>
          <div class="grid grid-cols-2 gap-4 mb-4">
            <label class="font-medium pl-8">Gender:</label>
            <p>{{ selectedUser.gender.charAt(0).toUpperCase() + selectedUser.gender.slice(1) }}</p>
          </div>
          <div class="grid grid-cols-2 gap-4 mb-4">
            <label class="font-medium pl-8">Country:</label>
            <p>{{ selectedUser.location.country }}</p>
          </div>
          <div class="grid grid-cols-2 gap-4 mb-4">
            <label class="font-medium pl-8">Email:</label>
            <p>{{ selectedUser.email }}</p>
          </div>
        </div>
      </Dialog>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from "vue";
import Dialog from "primevue/dialog";
import Header from "./components/Header.vue";
import DataTable from "primevue/datatable";
import Column from "primevue/column";
import Button from "primevue/button";
import InputText from "primevue/inputtext";
import Profile from "./components/Profile.vue";
import { RefreshCw } from 'lucide-vue-next';

const users = ref([]);
const searchQuery = ref("");
const selectedUser = ref(null);

const fetchUsers = async () => {
  try {
    const response = await fetch("https://randomuser.me/api/?results=20");
    const data = await response.json();
    users.value = data.results;
  } catch (error) {
    console.error("Error fetching users:", error);
  }
};

onMounted(fetchUsers);

const filteredUsers = computed(() => {
  return users.value.filter((user) =>
    `${user.name.first} ${user.name.last}`
      .toLowerCase()
      .includes(searchQuery.value.toLowerCase())
  );
});

const convertDate = (dateString) => {
  if (!dateString) return "N/A"; // Handle empty/null cases
  const dateObj = new Date(dateString);
  const day = dateObj.getDate().toString().padStart(2, "0"); // Ensures two-digit day
  const month = dateObj.toLocaleString("en-US", { month: "long" });
  const year = dateObj.getFullYear();
  return `${day} ${month} ${year}`;
};

const openModal = (user) => {
  selectedUser.value = user.data;
};
</script>

<style scoped>
.custom-table :deep(.p-datatable) {
  display: flex;
  flex-direction: column;
}

.custom-table :deep(.p-datatable-header-cell){
  border: none;
}

.custom-table :deep(.p-datatable-thead > tr) {
  display: flex;
  padding: 12px;
}

.custom-table :deep(.p-datatable-thead > tr > th),
.custom-table :deep(.p-datatable-tbody > tr > td) {
  flex: 1;
  text-align: left;
  padding: 12px;
}

.custom-table :deep(.p-datatable-tbody > tr) {
  display: flex;
  flex-direction: row;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin: 10px 0;
  padding: 12px;
}

.custom-table :deep(.p-datatable-tbody > tr > td) {
  border: none;
}

/* Hover effect */
.custom-table :deep(.p-datatable-tbody > tr:hover) {
  box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.15);
  transform: translateY(-2px);
}
</style>
