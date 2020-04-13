<template>
  <div>
    Todo予定地
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'

// defineComponentを使うことで型推論が効くようになるらしい
export default defineComponent({
  setup () {
    console.log('hello world')
  }
})
</script>
