<template>
  <div id="app">
    <h1>Chat</h1>
    <Chat :user1="user1" :user2="user2" />
  </div>
</template>

<script>
import axios from "axios";
import Chat from "./components/Chat.vue"; // Importamos el componente Chat

export default {
  data() {
    return {
      user1: null, 
      user2: null, 
    };
  },
  components: {
    Chat,
  },
  mounted() {
    
    axios.get("https://randomuser.me/api/?results=2")
      .then((response) => {
       
        this.user1 = response.data.results[0];
        this.user2 = response.data.results[1];
      })
      .catch((error) => {
        console.error("Error al cargar los usuarios:", error);
      });
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
}
</style>