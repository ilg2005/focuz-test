<template>
  <div class="container mx-auto p-4">
    <draggable v-model="categoriesWithMeals" tag="ul" itemKey="category" group="categories" handle=".handle1"
               animation="300">
      <template #item="{ element: categoryWithMeals }">
        <div>
          <div class="bg-gray-100 p-2 rounded mb-4 shadow relative">
            <div class="flex self-center">
              <div @click="toggleVisibility(categoryWithMeals)">
                <FoldButton v-if="categoryWithMeals.isVisible" class="mr-2"/>
                <UnfoldButton v-else class="mr-2"/>
              </div>
              <span>{{ categoryWithMeals.category }}</span>
            </div>
            <MoveButton class="handle1 top-4 right-5"/>
          </div>

          <draggable v-if="categoryWithMeals.isVisible" v-model="categoryWithMeals.meals" tag="ul" itemKey="meal" group="meals" class="mb-4 mr-0 flex-grow w-[95%] mx-auto"
                     handle=".handle2" animation="300">
            <template #item="{ element: meal }">
              <div class="bg-green-200 p-2 rounded mb-2 shadow relative">
                {{ meal }}
                <MoveButton class="handle2 top-1/2 transform -translate-y-1/2"/>
              </div>
            </template>
          </draggable>
        </div>
      </template>
    </draggable>
  </div>
</template>

<script setup>
import {ref} from 'vue';
import draggable from 'vuedraggable';
import MoveButton from "@/components/MoveButton.vue";
import FoldButton from "@/components/FoldButton.vue";
import UnfoldButton from "@/components/UnfoldButton.vue";

const categoriesWithMeals = ref([
  {
    category: 'Favorite Foods',
    meals: ['Hamburger', 'Pizza', 'Spaghetti', 'Tacos', 'Teriyaki Chicken'],
    isVisible: true,
  },
  {
    category: 'Terrible Foods',
    meals: ['Bat wing soup', 'Spicy Octopus', 'Anything from Taco Bell'],
    isVisible: true,
  }
]);


const toggleVisibility = (categoryWithMeals) => {
  categoryWithMeals.isVisible = !categoryWithMeals.isVisible;
};
</script>
