<template>
  <li>{{item.text}}</li>
</template>

<script lang="ts">
import { defineComponent, PropType } from '@vue/composition-api'
import { TodoItemType } from '@/views/TodoPage/index.vue'

export default defineComponent({
  props: {
    item: {
      type: Object as PropType<TodoItemType>,
      required: true
    }
  },
  setup () {
    console.log('')
  }
})
</script>
