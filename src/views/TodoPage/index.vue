<template>
  <div>
    <AddItemWrapper @addItem="addTodoItem" />
    <TodoList :todoList="state.todoList" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from '@vue/composition-api'
import TodoList from '@/components/TodoList/index.vue'
import AddItemWrapper from '@/components/AddItemWrapper/index.vue'

export type TodoItemType = {
  id: number;
  text: string;
  doneFlg: boolean;
}

// defineComponentを使うことで型推論が効くようになるらしい
// composition-apiv0.4.0でcreateComponentからdefineComponentに名前が変わった
export default defineComponent({
  components: {
    TodoList,
    AddItemWrapper
  },
  setup () {
    const state = reactive({
      todoList: [] as TodoItemType[]
    })
    for (let i = 0; i < 10; i++) {
      state.todoList.push({ id: i, text: 'todoItem' + i, doneFlg: false })
    }

    /** Todoリストに追加する */
    const addTodoItem = (text: string) => {
      const id = state.todoList.length
      console.log(id, text)
      state.todoList.push({ id, text, doneFlg: false })
    }

    return { state, addTodoItem }
  }
})
</script>
