<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="3">
        <v-card>
          <v-card-title>Filters</v-card-title>
          <v-card-text>
            <v-form>
              <v-select
                v-model="gender"
                :items="['All', 'Male', 'Female']"
                label="Gender"
              ></v-select>

              <v-divider></v-divider>

              <v-checkbox
                v-model="categories.all"
                label="All"
                @change="toggleCategories('all')"
              ></v-checkbox>
              <v-checkbox
                v-model="categories.kitchen"
                label="Kitchen"
                @change="toggleCategories('kitchen')"
              ></v-checkbox>
              <v-checkbox
                v-model="categories.electronics"
                label="Electronics"
                @change="toggleCategories('electronics')"
              ></v-checkbox>

              <v-divider></v-divider>

              <v-checkbox-group v-model="colors" label="Colors">
                <v-checkbox label="Red" value="red"></v-checkbox>
                <v-checkbox label="Blue" value="blue"></v-checkbox>
                <v-checkbox label="Green" value="green"></v-checkbox>
              </v-checkbox-group>

              <v-divider></v-divider>

              <v-radio-group v-model="priceRange" label="Price">
                <v-radio label="$10 - $50" value="10-50"></v-radio>
                <v-radio label="$50 - $100" value="50-100"></v-radio>
                <v-radio label="$100 - $150" value="100-150"></v-radio>
                <v-radio label="$150 - $200" value="150-200"></v-radio>
                <v-radio label="Over $200" value="200+"></v-radio>
              </v-radio-group>

              <v-divider></v-divider>

              <v-rating v-model="rating" label="Rating" :max="5"></v-rating>

              <v-btn @click="resetFilters">Reset Filters</v-btn>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>

      <v-col cols="12" md="9">
        <v-row>
          <v-col v-for="product in products" :key="product.id" cols="12" md="4">
            <v-card>
              <v-img :src="product.image" height="200px"></v-img>
              <v-card-title>{{ product.name }}</v-card-title>
              <v-card-subtitle
                >\${{ product.price }}
                <s>\${{ product.originalPrice }}</s></v-card-subtitle
              >
              <v-rating v-model="product.rating" :max="5" readonly></v-rating>
              <v-card-actions>
                <v-btn icon>
                  <v-icon>mdi-cart</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const gender = ref(null);
const categories = ref({
  all: true,
  kitchen: false,
  electronics: false,
});
const colors = ref([]);
const priceRange = ref(null);
const rating = ref(null);

const products = ref([
  {
    id: 1,
    name: "MacBook Air Pro",
    price: 15,
    originalPrice: 32,
    rating: 4,
    image:
      "https://product.hstatic.net/200000195587/product/quan-dui-bo-doi_0546eacc165c4980a2f8e6298ec143b6_master.jpg",
  },
  {
    id: 2,
    name: "Red Velvet Dress",
    price: 16,
    originalPrice: 14.59,
    rating: 5,
    image: "https://pos.nvncdn.com/c1bbe5-93650/ps/20230723_IO5UTkV4Im.jpeg",
  },
  {
    id: 3,
    name: "Boat Headphone",
    price: 36,
    originalPrice: 29,
    rating: 4,
    image:
      "https://bizweb.dktcdn.net/thumb/1024x1024/100/467/909/products/o1cn01qeydxa1uame6ibkg4-29376760-31360b92-84a2-4181-a2d3-608fdf53eae7.jpg?v=1723368389190",
  },
  {
    id: 4,
    name: "The Psychology of Money",
    price: 85,
    originalPrice: 499,
    rating: 5,
    image:
      "https://product.hstatic.net/1000063620/product/iphone-13-pro-xanh_2aaf47e4074c47559f5e3a5f592e998e_large_a3845ef5cf1a4c58b320989f3805ddd9.jpg",
  },
  {
    id: 5,
    name: "Psalms Book for Growth",
    price: 89,
    originalPrice: 99,
    rating: 4,
    image: "https://pos.nvncdn.com/c1bbe5-93650/ps/20230723_IO5UTkV4Im.jpeg",
  },
  {
    id: 6,
    name: "Gaming Console",
    price: 99,
    originalPrice: 86,
    rating: 5,
    image: "https://pos.nvncdn.com/c1bbe5-93650/ps/20230723_IO5UTkV4Im.jpeg",
  },
]);

const toggleCategories = (category) => {
  if (category === "all") {
    categories.value.kitchen = false;
    categories.value.electronics = false;
  }
};

const resetFilters = () => {
  gender.value = null;
  categories.value = { all: true, kitchen: false, electronics: false };
  colors.value = [];
  priceRange.value = null;
  rating.value = null;
};
</script>

<style scoped>
.v-card {
  margin-bottom: 20px;
}
</style>
