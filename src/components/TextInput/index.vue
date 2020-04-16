<template>
  <input type="text" @input="changeText" :value="inputText ">
</template>

<script lang="ts">
import { defineComponent, computed } from '@vue/composition-api'

export default defineComponent({
  props: {
    text: {
      type: String,
      required: true
    }
  },
  setup (props, { emit }) {
    // computedを挟まないと、親でpropsの値が変わっても反映されない
    const inputText = computed(() => props.text)
    const changeText = (e: InputEvent) => {
      emit('input', (e.target as HTMLInputElement).value)
    }
    return {
      inputText,
      changeText
    }
  }
})
</script>
