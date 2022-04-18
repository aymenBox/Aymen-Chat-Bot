<template>


    <q-scroll-area style="height: 65vh;,max-height: 65vh" ref="ChatScrollArea">
        <q-chat-message v-for="m in chat" :key="m.id" :name="m.name" :avatar="m.avatar" :text="m.text" :sent="m.sent" />
    </q-scroll-area>



    <!-- this q-input is for writing messages -->
    <div class="absolute-bottom q-pb-xl q-pl-md ">
        <q-input label="Write a message" outlined v-model="message" @keydown.enter="SendMessage()">
            <template v-slot:after>
                <q-btn dense flat icon="send" @click="SendMessage()" />
            </template>
        </q-input>
    </div>




</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
    name: 'ChatContainer',
    setup() {
        //set ScrollerOffset to -1 to prevent loading on initial load
        var ScrollerOffset = ref(-1);
        var messageId = 0;
        var chat = ref([
            {
                id: messageId++,
                name: 'aymen',
                avatar: '/bot.jpg',
                text: ['Hello I\'m a chat Bot My name is Aymen, how can i Help you Today'],
                sent: false
            }
        ]);
        var message = ref('');

        return {
            ScrollerOffset,
            message,
            chat,
            onLoad(index, done) {
                //ToDo: add loading spinner
            },
            SendMessage() {
                //ToDo: add message to chat
                console.log("user : ", message.value);
                //add message to chat
                chat.value.push({
                    id: messageId++,
                    name: 'user',
                    avatar: 'https://cdn.quasar.dev/img/avatar1.jpg',
                    text: [message.value],
                    sent: true
                });
                //after sending message, reset message to empty
                message.value = '';
                //set Scroll percentage to 100 every time a message is sent
                this.$refs.ChatScrollArea.setScrollPercentage("vertical", 100, 0);
            }
        }
    }
})
</script>
