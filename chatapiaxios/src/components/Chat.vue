<template>
  <div class="chat-container">
    <div v-if="user1 && user2" class="chat">
      <div class="users">
        <div class="user user-left">
          <img :src="user1.picture.thumbnail" alt="Avatar Usuario 1" class="user-avatar" />
          <p>{{ user1.name.first }} {{ user1.name.last }}</p>
        </div>
        <div class="user user-right">
          <img :src="user2.picture.thumbnail" alt="Avatar Usuario 2" class="user-avatar" />
          <p>{{ user2.name.first }} {{ user2.name.last }}</p>
        </div>
      </div>
      
      <div class="messages">
        <div
          v-for="message in messages"
          :key="message.id"
          :class="{'left': message.sender === user1.name.first, 'right': message.sender === user2.name.first, 'user1-message': message.sender === user1.name.first, 'user2-message': message.sender === user2.name.first}"
          class="message"
        >
          <img :src="message.avatar" alt="Avatar" class="avatar" />
          <div class="message-content">
            <strong>{{ message.sender }}:</strong> {{ message.text }}
          </div>
        </div>
      </div>

      <div class="input-section">
        <input v-model="newMessage" placeholder="Escribe un mensaje..." />
        <button @click="sendMessage(user1)">Enviar como {{ user1.name.first }}</button>
        <button @click="sendMessage(user2)">Enviar como {{ user2.name.first }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    user1: Object, 
    user2: Object, 
  },
  data() {
    return {
      messages: [], 
      newMessage: "", 
      messageColor: "#ffffff", 
    };
  },
  methods: {
    sendMessage(user) {
      if (this.newMessage.trim() === "") return; 

      const message = {
        id: Date.now(),
        sender: `${user.name.first}`,
        text: this.newMessage,
        color: this.messageColor,
        avatar: user.picture.thumbnail, 
      };

      this.messages.push(message);

      this.newMessage = "";
    },
  },
};
</script>

<style scoped>
.chat-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.chat {
  width: 400px;
  border: 2px solid #d3d3d3;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
}

.header {
  background-color: #0078d7;
  color: white;
  padding: 10px;
  text-align: center;
  font-size: 1.2em;
}

.users {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  background-color: #e5e5e5;
  align-items: center;
}

.user {
  display: flex;
  align-items: center;
  font-size: 0.9em;
}

.user-left {
  justify-content: flex-start;
}

.user-right {
  justify-content: flex-end;
}

.user-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 8px;
}

.messages {
  padding: 10px;
  height: 250px;
  overflow-y: auto;
  background-color: #f0f0f0;
}

.message {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 15px;
  max-width: 80%;
  word-wrap: break-word;
}

.user1-message {
  background-color: #ffffff;
  color: #000;
  justify-content: flex-start;
}

.user2-message {
  background-color: #d1e7fd;
  color: #000;
  justify-content: flex-end;
  flex-direction: row-reverse;
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin: 0 10px;
}


.input-section {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  background-color: #d3d3d3;
}

input[type="text"] {
  flex: 1;
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

input[type="color"] {
  width: 30px;
  height: 30px;
  border: none;
  cursor: pointer;
}

button {
  padding: 5px 10px;
  background-color: #0078d7;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #005fa3;
}
</style>
