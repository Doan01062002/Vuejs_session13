<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Product List</h1>
        <v-text-field
          v-model="search"
          label="Search"
          append-icon="mdi-magnify"
          single-line
          hide-details
        ></v-text-field>
        <v-btn color="primary" @click="addNewItem">Add New Item</v-btn>
        <v-data-table
          :headers="headers"
          :items="filteredItems"
          :items-per-page="5"
          class="elevation-1"
        >
          <template v-slot:top>
            <v-toolbar flat>
              <v-toolbar-title>Product List</v-toolbar-title>
            </v-toolbar>
          </template>
          <template v-slot:item.status="{ item }">
            <v-chip :color="item.status === 'In stock' ? 'green' : 'red'" dark>
              {{ item.status }}
            </v-chip>
          </template>
          <template v-slot:item.actions="{ item }">
            <v-icon @click="editItem(item)">mdi-pencil</v-icon>
            <v-icon @click="deleteItem(item)">mdi-delete</v-icon>
          </template>
        </v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, computed } from "vue";

const search = ref("");
const items = ref([
  {
    image: "path/to/image1.jpg",
    product: "Curology Face wash",
    date: "Thu, Jan 12 2023",
    status: "In stock",
    price: 275,
  },
  {
    image: "path/to/image2.jpg",
    product: "Body Lotion",
    date: "Thu, Jan 20 2023",
    status: "Out of Stock",
    price: 89,
  },
  {
    image: "path/to/image3.jpg",
    product: "Smart Watch",
    date: "Fri, Feb 15 2024",
    status: "In stock",
    price: 125,
  },
  {
    image: "path/to/image4.jpg",
    product: "Camera",
    date: "Fri, March 30 2024",
    status: "In stock",
    price: 200,
  },
  {
    image: "path/to/image5.jpg",
    product: "Games",
    date: "Sat, March 30 2024",
    status: "Out of Stock",
    price: 100,
  },
]);

const headers = [
  { text: "Product Image", value: "image", sortable: false },
  { text: "Product", value: "product" },
  { text: "Date", value: "date" },
  { text: "Status", value: "status" },
  { text: "Price", value: "price", sortable: false },
  { text: "Actions", value: "actions", sortable: false },
];

const filteredItems = computed(() => {
  return items.value.filter((item) =>
    item.product.toLowerCase().includes(search.value.toLowerCase())
  );
});

const addNewItem = () => {
  // Logic to add a new item
};

const editItem = (item) => {
  // Logic to edit the item
};

const deleteItem = (item) => {
  // Logic to delete the item
};
</script>

<style scoped>
/* Thêm các kiểu tùy chỉnh nếu cần */
</style>
