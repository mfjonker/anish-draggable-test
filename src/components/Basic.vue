<template>
  <div class="flex justify-center">
    <div class="w-64">
      <!-- list #1 -->
      <draggable class="dragArea list-group w-full"
                 group="sortable-list-items"
                 v-model="state.list[0]"
                 :sort="true"
                 :move="checkMove">
        <div class="list-group-item bg-gray-300 m-1 p-3 rounded-md text-center cursor-pointer"
             v-for="element in state.list[0]"
             :key="element.name">
          {{ element.name }}
        </div>
      </draggable>
      <!-- list #2 -->
      <draggable class="dragArea list-group w-full"
                 group="sortable-list-items"
                 v-model="state.list[1]"
                 :sort="true"
                 :move="checkMove">
        <div class="list-group-item bg-gray-300 m-1 p-3 rounded-md text-center cursor-pointer"
             v-for="element in state.list[1]"
             :key="element.name">
          {{ element.name }}
        </div>
      </draggable>
    </div>
    <!-- display lists -->
    <div class="raw-displays">
      <rawDisplays class="w-64" :value="state.list[0]" />
      <rawDisplays class="w-64" :value="state.list[1]" />
    </div>  
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue'
// @ts-ignore
import { VueDraggableNext } from 'vue-draggable-next'
import rawDisplays from './rawDisplay.vue'
export default defineComponent({
  components: {
    draggable: VueDraggableNext,
    rawDisplays,
  },
  setup() {
    const state = reactive({
      list: [
        [
          { name: 'John', id: 1 },
          { name: 'Joao', id: 2 },
          { name: 'Jean', id: 3 },
          { name: 'Gerard', id: 4 }
        ],
        [
          { name: 'Marco', id: 1 },
          { name: 'Marcel', id: 2 },
          { name: 'Martin', id: 3 },
          { name: 'Michael', id: 4 }
        ]
      ]
    })
    function checkMove(evt) {
      console.log('Future index: ' + evt.draggedContext.futureIndex)
      console.log('element: ' + evt.draggedContext.element.name)
    }
    return {
      state,
      checkMove
    }
  },
})
</script>

<style scoped>
  .raw-displays {
    margin: 2rem;
  }
</style>
