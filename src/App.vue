<script setup>
  import { reactive, ref } from 'vue'
  import Contact from './components/Contact.vue'
  import Form from './components/Form.vue'
  import { onMounted } from 'vue'
  import axios from 'axios'
  import { API_ENDPOINTS, API_HOST } from "./constants/config.js"

  const contactList = ref([])
  let errorMessage = ref('')

  onMounted(() => {
    getUsers()
  })

  async function getUsers() {
      try{
          var response = await axios.get(API_HOST+API_ENDPOINTS.contact)
          if(response.status == 200) {
              contactList.value = response.data
          }
      } catch(exception) {
          errorMessage.value = exception.response.data.message
      }
  }
</script>

<template>
  <h1>Formulaure d'ajout</h1>
  <Form />
  <h1>Liste des contacts</h1>
  <Contact v-for="item in contactList" v-bind="item"  />
</template>
