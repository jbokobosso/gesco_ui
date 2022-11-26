<script setup>
    import { reactive, ref } from 'vue'
    import axios from 'axios'
    import { API_ENDPOINTS, API_HOST } from "../constants/config.js"

    const props = defineProps({
        _id: String,
        firstname: String,
        lastname: String,
        phone: String,
        email: String
    })
  
    let errorMessage = ref('')

    async function deleteContact() {
      try{
          var response = await axios.delete(API_HOST+API_ENDPOINTS.contact+"/"+props._id)
          if(response.status == 200) {
            errorMessage.value = ''
            alert('Contact supprié')
            window.location.href = '/'
          }
      } catch(exception) {
          errorMessage.value = exception.response.data.message
      }
  }
</script>

<template class="card-container">
    <div class="card">
        <h1 id="name">{{firstname}} {{lastname.toUpperCase()}}</h1>
        <div id="card-items">
            <div id="avatar"></div>
            <div id="infos">
                <a id="phone" href="tel:{{phone}}">{{phone}}</a>
                <span id="email">{{email}}</span>
            </div>
        </div>
        <button @click="deleteContact" id="suppress">Supprimer</button>
    </div>
    <p id="error-message" v-if="errorMessage != ''">
        {{errorMessage}}
    </p>
</template>

<style>

body {
    background-color: #E2EEF7;
}

template {
}

#suppress {
    margin-top: 9px;
    border: none;
    background-color: #282B34;
    color: white;
    border-radius: 20px;
}

.card {
    padding-left: 40px;
    background-color: rgb(255, 255, 255);
    width: 80%;
    margin: auto;
    border-radius: 20px;
    color: #282B34;
    padding-bottom: 20px;
    padding-top: 10px;
    box-shadow: 1px 1px 10px#282B34;
}

#infos {
    display: flex;
    flex-direction: column;
}

#avatar {
    background-image: url("../assets/profile.png");
    border-radius: 50px;
    width: 50px;
    height: 50px;
    background-size: cover;
}

@media only screen and (max-width: 700px) {
    #name {
        font-size: 1em;
    }
    .card {
    margin-top: 50px;
        width: 80%;
    }
    #email, #phone {
        margin-left: 30px;
    }
    #avatar img {
        width: 100%;
    }
    .card-items {
        display: flex;
    }
}

@media only screen and (min-width: 700px){
    #name {
        font-size: 1.5em;
    }
    .card {
    margin-top: 50px;
        width: 50%;
    }
    #email, #phone {
        margin-left: 30px;
    }
    #avatar img {
        width: 100%;
    }
    .card-items {
        display: flex;
    }
}
</style>