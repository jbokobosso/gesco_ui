<script setup>
    import { reactive, ref } from 'vue'
    import axios from 'axios'
    import { API_ENDPOINTS, API_HOST } from "../constants/config.js"

 

    let errorMessage = ref('')
    const firstname = ref('')
    const lastname = ref('')
    const phone = ref('')
    const email = ref('')

    function handleForm() {
        const formValue = {
            firstname: firstname.value,
            lastname: lastname.value,
            phone: phone.value,
            email: email.value
        }
        createUser(formValue)
    }

    async function createUser(formValue) {
        try{
            var response = await axios.post(API_HOST+API_ENDPOINTS.contact, formValue, { contentType: 'JSON' })
            if(response.status == 200) {
                formValue = {}
                errorMessage.value = ""
                alert("Merci !")
                window.location.href = "/"
            }
        } catch(exception) {
            errorMessage.value = exception.response.data.message
        }
    }
</script>

<template>
    <form @submit.prevent="onSubmit" v-on:submit="handleForm">
        <label for="firstname">Prénom</label>
        <input type="text" id="firstname" v-model="firstname" placeholder="Ex: John" />
        
        <label for="lastname">Nom</label>
        <input type="text" id="lastname" v-model="lastname" placeholder="Ex: DOE" />
        
        <label for="phone">Téléphone</label>
        <input type="tel" id="phone" v-model="phone" placeholder="Ex: +228 99 88 58 25" />
        
        <label for="email">E-mail</label>
        <input type="email" id="email" v-model="email" placeholder="Ex: john.do@example.com" />
        
        <input type="submit" value="Ajouter">
    </form>
    <p id="error-message" v-if="errorMessage != ''">
        {{errorMessage}}
    </p>
</template>

<style>
#error-message {
    color: red;
    font-weight: bold;
    text-align: center;
}

form {
  display: flex;
  flex-direction: column;
  width: 50%;
  margin: auto;
}

input {
  margin-bottom: 20px;
}
</style>