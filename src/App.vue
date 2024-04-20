<template>
  <div class="container mx-auto p-4">
    <draggable v-model="categoriesWithDocs" tag="ul" itemKey="category" group="categories" handle=".handle1"
               animation="300">
      <template #item="{ element: categoriesWithDocs }">
        <li>
          <div class="p-2 border relative">
            <div class="flex self-center">
              <div @click="toggleVisibility(categoriesWithDocs)">
                <FoldButton v-if="categoriesWithDocs.isVisible" class="mr-2"/>
                <UnfoldButton v-else class="mr-2"/>
              </div>
              <span class="font-bold">{{ categoriesWithDocs.category }}</span>
            </div>
            <MoveButton class="handle1 top-4 right-5"/>
          </div>

          <draggable v-if="categoriesWithDocs.isVisible" v-model="categoriesWithDocs.docs" tag="ul" itemKey="doc" group="docs" class="mr-0 flex-grow w-[95%] mx-auto"
                     handle=".handle2" animation="300">
            <template #item="{ element: doc }">
              <li class="p-2 border relative">
                {{ doc }}
                <MoveButton class="handle2 top-1/2 transform -translate-y-1/2"/>
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

const categoriesWithDocs = ref([
  {
    category: 'Обязательные для всех',
    docs: ['Паспорт', 'ИНН'],
    isVisible: true,
  },
  {
    category: 'Обязательные для трудоустройства',
    docs: ['Заявление о приеме на работу', 'Трудовой договор', 'Правила внутреннего распорядка'],
    isVisible: true,
  },
  {
    category: 'Специальные',
    docs: ['Специальный документ 1', 'Специальный документ 2'],
    isVisible: true,
  },

]);


const toggleVisibility = (categoriesWithDocs) => {
  categoriesWithDocs.isVisible = !categoriesWithDocs.isVisible;
};
</script>
