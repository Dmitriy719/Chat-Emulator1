<template>
    <div class="container">
        <div class="chat-box" v-for="(chat, index) in chats" :key="index">
            <h2>{{ chat.name }}</h2>
            <div class="messages">
                <div
                v-for="(message, messageIndex) in chat.messages"
                :key="messageIndex"
                :class="{'sent': message.sender===chat.name}">
                    {{ message.content }}
                </div>
            </div>
            <div class="input-area">
                <input type="text" v-model="newMessage"
                placeholder="Введите сообщение">
                <button
                @click="sendMessage(chat.name)">Отправить</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue'

const chats = ref([
    {
        name: 'User 1',
        messages: [],
    },
    {
        name: 'User 2',
        messages: [],
    },
]);

const newMessage = ref('');

const sendMessage = (sender) =>{
    const message = {
        sender,
        content: newMessage.value
    };

    chats.value.forEach(chat =>{
        chat.messages.push(message)
    });

    newMessage.value = '';
};

</script>

<style scoped>
.container {
    display:flex;
    gap: 20px;
}

.chat-box {
    border: 1px solid #ccc;
    padding: 20px;
    width: 300px;
}

.messages {
    height: 200px;
    overflow-y: auto;
    margin-bottom: 10px;
}

.messages div {
    margin-bottom: 5px;
    padding: 8px 12px;
    border-radius: 8px;
}

.sent {
    background-color: #e0f2f7;
    text-align: right;
}

.input-area {
    display: flex;
    gap: 10px;
}
</style>