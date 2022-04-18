<template>
    <div class="q-pa-md">
        <q-infinite-scroll @load="onLoad" reverse :offset="-1">
            <template v-slot:loading>
                <div class="row justify-center q-my-md">
                    <q-spinner color="primary" name="dots" size="40px" />
                </div>
            </template>
            <div id="MyChatMessageContainer">
                <q-chat-message name="aymen" avatar="~assets/bot.jpg"
                    :text="['Hello I\'m a chat Bot My name is Aymen, how can i Help you Today']" />
                <q-chat-message name="User" avatar="https://cdn.quasar.dev/img/avatar1.jpg" :text="['hey, how are you?']"
                    sent />

            </div>

        </q-infinite-scroll>
        <!-- this q-input is for writing messages -->
        <div class="absolute-bottom q-pb-xl q-pl-md">
            <q-input label="Write a message" outlined>
                <template v-slot:after>
                    <q-btn dense flat icon="send" @click="SendMessage()" />
                </template>
            </q-input>
        </div>

    </div>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
    name: 'ChatContainer',
    setup() {
        //set ScrollerOffset to -1 to prevent loading on initial load
        var ScrollerOffset = ref(-1);
        var chat = ref([]);

        return {
            ScrollerOffset,
            onLoad(index, done) {
                //ToDo: add loading spinner
            },
            SendMessage() {
                //ToDo: add message to chat
            }
        }
    }
})
</script>
