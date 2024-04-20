<template>
  <div class="container">
    <draggable v-model="categories"
               tag="ul"
               itemKey="title"
               group="categories"
               handle=".handle-cat"
               animation="300"
               ghostClass="ghost-el"

    >
      <template #item="{ element: category }">
        <li>
          <div class="px-4 py-2 border relative">
            <div class="flex">
              <div @click="toggleVisibility(category)">
                <FoldButton v-if="category.isVisible" class="mr-2"/>
                <UnfoldButton v-else class="mr-2"/>
              </div>
              <span class="px-2 font-bold">{{ category.title }}</span>
            </div>
            <MoveButton class="handle handle-cat"/>
          </div>

          <draggable v-if="category.isVisible"
                     v-model="category.docs"
                     tag="ul"
                     itemKey="doc"
                     group="docs"
                     class="pl-4 flex-grow max-w-[1144px]"
                     handle=".handle-doc"
                     animation="300"
                     ghostClass="ghost-el"
                     chosenClass="chosen-el"
          >
            <template #item="{ element: doc }">
              <li class="px-4 py-2 border relative">
                {{ doc }}
                <MoveButton class="handle handle-doc"/>
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
