<template>
  <button @click="clickEvent">{{buttonText}}</button>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  props: {
    text: {
      type: String,
      required: true
    }
  },
  setup (props, { emit }) {
    const clickEvent = () => {
      emit('click')
    }
    return {
      buttonText: props.text,
      clickEvent
    }
  }
})
</script>
