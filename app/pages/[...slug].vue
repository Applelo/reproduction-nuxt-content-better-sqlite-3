<script setup lang="ts">
const route = useRoute()

const { data: page, error, execute } = await useAsyncData('page-' + route.path, () => {
  return queryCollection('content').path(route.path).first()
})
</script>

<template>
  <div>
    <ContentRenderer
      v-if="page"
      :value="page"
    />
    <div v-else-if="error">
      <h2>Error</h2>
      <p>Message: {{ error.message }}</p>
      <p>Data: {{ error.data }}</p>
      <p>Cause: {{ error.cause }}</p>
      <button @click="execute()">Fetch on client side</button>
    </div>
  </div>
</template>
