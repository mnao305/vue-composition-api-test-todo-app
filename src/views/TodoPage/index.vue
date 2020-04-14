<template>
  <div>
    <TodoList :todoList="state.todoList" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from '@vue/composition-api'
import TodoList from '@/components/TodoList/index.vue'

export type TodoItemType = {
  id: number;
  text: string;
  doneFlg: boolean;
}

// defineComponentを使うことで型推論が効くようになるらしい
// composition-apiv0.4.0でcreateComponentからdefineComponentに名前が変わった
export default defineComponent({
  components: {
    TodoList
  },
  setup () {
    const state = reactive({
      todoList: [] as TodoItemType[]
    })
    for (let i = 0; i < 10; i++) {
      state.todoList.push({ id: i, text: 'todoItem' + i, doneFlg: false })
    }

    return { state }
  }
})
</script>
