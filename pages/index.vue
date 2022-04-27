<template>
  <pre>token: {{ token }}</pre>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data: () => ({
    token: window.localStorage.getItem('access_token'),
  }),
})
</script>
