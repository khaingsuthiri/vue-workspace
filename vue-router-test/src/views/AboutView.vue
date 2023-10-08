<script setup lang="ts">
import { watch } from 'vue'
import { onBeforeRouteLeave, onBeforeRouteUpdate, useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()

const goToNext = () => {
  router.push('/about/2')
}

watch(
  () => route.params.id,
  (newId) => {
    console.log('Watching ...', newId)
  }
)

onBeforeRouteLeave((to, from) => {
  console.log(to)
  console.log(from)

  const answer = window.confirm('Do you really want to go home?')
  if (!answer) return false
})

onBeforeRouteUpdate((to, from) => {
  if (to.params.id !== from.params.id) {
    console.log(from.params.id, ' to ', to.params.id)
  }
})
</script>

<template>
  <h1>This is about.</h1>
  <p>ID : {{ route.params.id }}</p>
  <p>
    Lorem ipsum, dolor sit amet consectetur adipisicing elit. Iure iste doloribus sequi ut
    doloremque et harum natus tenetur dolorum unde quaerat repellat dolor quae cumque, quidem animi
    modi, illo nemo.
  </p>
  <button @click="goToNext">Next</button>
</template>
