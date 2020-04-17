<template>
  <input type="text" v-model="inputText ">
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
    const inputText = computed({
      get: () => props.text,
      set: (value) => emit('input', value)
    })
    return {
      inputText
    }
  }
})
</script>
