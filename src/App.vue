<script setup>
  import { reactive, ref } from 'vue'
  import Contact from './components/Contact.vue'
  import Form from './components/Form.vue'

  const state = reactive({ count: 0 })
  const contactList = ref([1,5,4,5,8,9,6,3,2,5])

  function increment() {
    state.count++
  }
</script>

<template>
  <h1>Formulaure d'ajout</h1>
  <Form />
  <h1>Liste des contacts</h1>
  <Contact v-for="item in contactList" />
</template>
