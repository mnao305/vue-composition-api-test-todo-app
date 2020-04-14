<template>
<ul>
  <TodoItem v-for="v in todoList" :item="v" :key="v.id" />
</ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from '@vue/composition-api'
import TodoItem from '@/components/TodoItem/index.vue'
import { TodoItemType } from '@/views/TodoPage/index.vue'

export default defineComponent({
  components: {
    TodoItem
  },
  props: {
    todoList: {
      // PropTypeで型をちゃんと指定できる
      type: Array as PropType<TodoItemType[]>,
      require: true
    }
  },
  setup (props) {
    console.log(props.todoList)
  }
})
</script>
