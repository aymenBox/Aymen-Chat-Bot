<template>


    <q-scroll-area style="height: 65vh;,max-height: 65vh" ref="scrollAreaRef" horizontalPercentage="1">
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
import { api } from "boot/axios";

export default defineComponent({
    name: 'ChatContainer',
    setup() {
        //set ScrollerOffset to -1 to prevent loading on initial load
        var ScrollerOffset = ref(-1);
        var messageId = 0;
        const scrollAreaRef = ref(null)
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
            scrollAreaRef,
            chat,
            onLoad(index, done) {
                //ToDo: add loading spinner
            },
            SendMessage() {
                //ToDo: add message to chat
                console.log("user : ", message.value);

                //add user message to chat
                chat.value.push({
                    id: messageId++,
                    name: 'user',
                    avatar: 'https://cdn.quasar.dev/img/avatar1.jpg',
                    text: [message.value],
                    sent: true
                });

                //send get request to http://127.0.0.1:5000/chatbot?question=message.value
                //get response from server
                api.get('/chatbot?question=' + message.value)
                    .then(response => {
                        chat.value.push({
                            id: messageId++,
                            name: 'aymen',
                            avatar: '/bot.jpg',
                            text: [response.data.responce],
                            sent: false
                        });
                        //this.$refs.ChatScrollArea.setScrollPercentage("vertical", 100, 0);
                        message.value = '';

                        setTimeout(function () {
                            scrollAreaRef.value.setScrollPercentage("vertical", 5000, 0);
                            //your code here
                        }, 100);

                    })
                    .catch(error => {
                        console.log("error : ", error);
                    });
                message.value = '';

            }
        }
    }
})
</script>
