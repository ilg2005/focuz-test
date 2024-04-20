<template>
  <div class="container mx-auto p-4">
    <draggable v-model="categories"
               tag="ul"
               itemKey="title"
               group="categories"
               handle=".handle-cat"
               animation="300">
      <template #item="{ element: category }">
        <li>
          <div class="p-2 border relative">
            <div class="flex self-center">
              <div @click="toggleVisibility(category)">
                <FoldButton v-if="category.isVisible" class="mr-2"/>
                <UnfoldButton v-else class="mr-2"/>
              </div>
              <span class="font-bold">{{ category.title }}</span>
            </div>
            <MoveButton class="handle-cat top-4 right-5"/>
          </div>

          <draggable v-if="category.isVisible"
                     v-model="category.docs"
                     tag="ul" itemKey="doc"
                     group="docs"
                     class="mr-0 flex-grow w-[95%] mx-auto"
                     handle=".handle-doc" animation="300">
            <template #item="{ element: doc }">
              <li class="p-2 border relative">
                {{ doc }}
                <MoveButton class="handle-doc top-1/2 transform -translate-y-1/2"/>
              </li>
            </template>
          </draggable>
        </li>
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

const categories = ref([
  {
    title: 'Обязательные для всех',
    docs: ['Паспорт', 'ИНН'],
    isVisible: true,
  },
  {
    title: 'Обязательные для трудоустройства',
    docs: ['Заявление о приеме на работу', 'Трудовой договор', 'Правила внутреннего распорядка'],
    isVisible: true,
  },
  {
    title: 'Специальные',
    docs: ['Специальный документ 1', 'Специальный документ 2'],
    isVisible: true,
  },

]);


const toggleVisibility = (category) => {
  category.isVisible = !category.isVisible;
};
</script>
