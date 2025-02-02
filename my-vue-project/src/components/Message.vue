<template>
    <div>
        <h1>Real-Time Messages</h1>
        <ul>
            <li v-for="(message, index) in messages" :key="index">{{ message }}</li>
        </ul>
    </div>
</template>

<script>
import { io } from "socket.io-client";

export default {
    data() {
        return {
            messages: [],  // List to hold incoming messages
            socket: null,   // Socket.io instance
        };
    },
    mounted() {
        // Connect to the Node.js server via Socket.io
        this.socket = io("http://localhost:3000");

        // Listen for the 'newMessage' event and update the message list
        this.socket.on("newMessage", (message) => {
            this.messages.push(message);  // Add received message to the list
        });
    },
};
</script>

<style scoped>
/* Optional: Add styles */
</style>