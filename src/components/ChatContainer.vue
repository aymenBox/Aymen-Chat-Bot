<template>
    <div class="q-pa-md">
        <q-infinite-scroll @load="onLoad" reverse :offset="-1">
            <template v-slot:loading>
                <div class="row justify-center q-my-md">
                    <q-spinner color="primary" name="dots" size="40px" />
                </div>
            </template>
            <div id="MyChatMessageContainer">
                <q-chat-message name="me" avatar="https://cdn.quasar.dev/img/avatar1.jpg" :text="['hey, how are you?']"
                    sent />
                <q-chat-message name="Jane" avatar="https://cdn.quasar.dev/img/avatar2.jpg"
                    :text="['doing fine, how r you?']" />
            </div>

        </q-infinite-scroll>
        <!-- this q-input is for writing messages -->
        <q-input label="Write a message" >
            <template v-slot:after>
                <q-btn round dense flat icon="send" />
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
        var ScrollerOffset = -1;

        return {
            ScrollerOffset,
            onLoad(index, done) {
                //ToDo: add loading spinner
            }
        }
    }
})
</script>
