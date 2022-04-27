<template>
  <section>
    <pre>token: {{ token }}</pre>
    <pre>me: {{ me }}</pre>
    <pre>result: {{ result }}</pre>
  </section>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data: () => ({
    token: window.localStorage.getItem('access_token'),
  }),

  async asyncData({ $axios }) {
    const me = await $axios.$get('/me', {
      headers: {
        Authorization: `Bearer ${window.localStorage.getItem('access_token')}`,
      },
    })

    const result = await $axios.$get('/result', {
      params: {
        studentID: 304,
      },
      headers: {
        Authorization: `Bearer ${window.localStorage.getItem('access_token')}`,
      },
    })

    return { me, result }
  },
})
</script>
