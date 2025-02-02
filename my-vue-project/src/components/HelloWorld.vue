<template>
  <div>
    <h1>List of Detected NFC Cards</h1>
    <p v-if="isLoading">Waiting for cards...</p>
    <ul>
      <li v-for="(card, index) in cardUids" :key="index">{{ card }}</li>
    </ul>
  </div>
</template>

<script>
import { io } from 'socket.io-client';

export default {
  data() {
    return {
      cardUids: [],  // Array to store detected card UIDs
      isLoading: true,  // Flag to show loading state
    };
  },
  mounted() {
    // Connect to the Socket.io server
    const socket = io('http://localhost:3000');  // Adjust URL as needed

    // Listen for the 'newCard' event sent from the server
    socket.on('newCard', (uid) => {
      // Add the card UID to the list
      this.cardUids.push(uid);

      // Change loading state when a card is detected
      if (this.isLoading) {
        this.isLoading = false;  // Hide loading message after first card detection
      }
    });
  },
};
</script>

<style scoped>
/* Basic styling */
h1 {
  font-size: 2em;
  color: #333;
}

ul {
  padding: 0;
  list-style-type: none;
}

li {
  background-color: #f4f4f4;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
  color: #000;
}

p {
  font-size: 1.2em;
  color: #999;
}
</style>
