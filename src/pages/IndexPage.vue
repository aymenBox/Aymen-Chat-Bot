<template>
  <q-page class="">
    <ChatContainer></ChatContainer>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import ChatContainer from 'src/components/ChatContainer.vue'

export default defineComponent({
  name: "IndexPage",
  components: { ChatContainer }
})
</script>
