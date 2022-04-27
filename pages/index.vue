<template>
  <section>
    <pre>result: {{ result }}</pre>
  </section>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',

  async asyncData({ $axios }) {
    const result = await $axios.$get('/api/result', {
      params: {
        studentID: 304,
      },
    })

    return { result }
  },
})
</script>
