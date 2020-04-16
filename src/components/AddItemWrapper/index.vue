<template>
  <div>
    <TextInput @input="changeText" :text="state.text" />
    <CustomButton @click="clickEvent" text="追加" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from '@vue/composition-api'
import TextInput from '@/components/TextInput/index.vue'
import CustomButton from '@/components/CustomButton/index.vue'

export default defineComponent({
  components: {
    TextInput,
    CustomButton
  },
  setup (_, context) {
    const state = reactive({
      text: ''
    })
    const changeText = (text: string) => {
      state.text = text
    }
    const clickEvent = () => {
      context.emit('addItem', state.text)
      changeText('')
    }
    return {
      clickEvent,
      changeText,
      state
    }
  }
})
</script>
