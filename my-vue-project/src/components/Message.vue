<template>
    <div class="p-4">
        <h1 class="h2 mb-4">Real-Time Messages</h1>
        <table class="table table-bordered table-striped">
            <thead>
                <tr>
                    <th scope="col">ID</th>
                    <th scope="col">Message</th>
                    <th scope="col">Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(message, index) in messages" :key="message.id">
                    <td>{{ message.id }}</td>
                    <td>{{ message.message }}</td>
                    <td>
                        <button @click="deleteMessage(message.id)" class="btn btn-danger">
                            Delete
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import http from "@/http"; // Import the configured Axios instance
import { io } from "socket.io-client"; // Import the socket.io client

export default {
    data() {
        return {
            messages: [],  // List to hold incoming messages
            socket: null,   // Socket.io instance
        };
    },
    mounted() {
        this.socket = io("http://localhost:3000");

        // Listen for the 'newMessage' event
        this.socket.on("newMessage", async (message) => {
            try {
                const storedMessage = await this.storeMessage(message);
                this.messages.push(storedMessage);
            } catch (error) {
                console.error("Error storing message:", error);
            }
        });

        // Listen for connection issues
        this.socket.on("connect_error", (err) => {
            console.error("Socket.io connect error:", err.message);
            alert("Connection lost. Trying to reconnect...");
        });

        this.socket.on("connect", () => {
            console.log("Connected to Socket.io server.");
        });

        // Fetch the list of messages
        this.fetchMessages();
    },
    methods: {
        async fetchMessages() {
            try {
                // Send a GET request to fetch the messages using the relative URL
                const response = await http.get("/api/messages");
                // Assuming the response data is an array of messages
                this.messages = response.data;
            } catch (error) {
                console.error("Error fetching messages:", error);
            }
        },

        // Method to delete a message
        async deleteMessage(messageId) {
            try {
                // Send a DELETE request to remove the message by its ID
                const response = await http.delete(`/api/messages/${messageId}`);
                console.log("Message deleted successfully:", response.data);

                // Remove the deleted message from the list
                this.messages = this.messages.filter((message) => message.id !== messageId);
            } catch (error) {
                console.error("Error deleting message:", error);
            }
        },

        async storeMessage(message, retries = 3) {
            try {
                const response = await http.post("/api/messages", { message: message });
                return response.data;
            } catch (error) {
                if (retries > 0) {
                    console.log("Retrying to store message...");
                    return this.storeMessage(message, retries - 1); // Retry the request
                } else {
                    console.error("Failed to store message:", error);
                    throw error;
                }
            }
        }
    },
};
</script>

<style scoped>
/* No additional styles are needed with Bootstrap */
</style>
