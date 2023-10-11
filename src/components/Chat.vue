<script setup>


import {computed, onMounted, ref, watch} from "vue";

const messages = ref([]);
const newMessage = ref('');
const socket = ref(null)
const status = ref("waiting")
const chatBox = ref(null)
const typing = ref(false)
const typingInterval = ref(null)
const onlineUsers = ref(0)
const isConnected = computed({
  get(){
    return status.value === "connected"
  }
})

const statusToText = computed({
  get(){
    const statuses = {
      "connected": "Connected",
      "disconnected": "Disconnected",
      "initial": "Initial",
      "waiting": "Waiting",
    }
    return  statuses[status.value]
  }
})

const makeTyping = () => {
  clearInterval(typingInterval.value)
  typing.value = true
  typingInterval.value = setTimeout(()=>{
    typing.value = false
  }, 1500)
}
const sendTyping = () => {
  if (socket.value){
    socket.value.send(JSON.stringify({ data: "typing" }));
  }
}
const setupWebSocket = () => {
  if (socket.value){
    socket.value.close()
    status.value = "waiting"
  }
  messages.value = []
  socket.value = new WebSocket('wss://server.privet.ge/ws');

  socket.value.addEventListener('open', (event) => {
    console.log('WebSocket connection opened:', event);
  });

  socket.value.addEventListener('message', (event) => {
    const parseMessage = JSON.parse(event.data);
    if (typeof parseMessage.data && parseMessage.data === "partner_connected"){
      status.value = "connected"
      messages.value = []
      const message = {class:"green system", text:"Partner Connected", date: new Date().toLocaleString()}
      messages.value.push(message);
    }else if (typeof parseMessage.data && parseMessage.data === "partner_disconnected"){
      status.value = "disconnected"
      const message = {class:"system", text:"Partner Disconnected", date: new Date().toLocaleString()}
      messages.value.push(message);
      socket.value.close()
    }else if(typeof parseMessage.data && parseMessage.data === "typing"){
      makeTyping()
    }else if(typeof parseMessage.online && parseMessage.online){
      onlineUsers.value = parseMessage.data
    }else{
      const message = {class:"partner", text:parseMessage.text, date: new Date().toLocaleString()}
      messages.value.push(message);
    }
    scrollToBottom()
    
  });

  socket.value.addEventListener('close', (event) => {
    console.log('WebSocket connection closed:', event);
  });
}
const sendMessage = () => {
  if (!isConnected.value)return
  if (!newMessage.value.length)return
  const message = {class:"me", text:newMessage.value, date: new Date().toLocaleString()}
  messages.value.push(message);
  if (newMessage.value.trim() !== '') {
    socket.value.send(JSON.stringify({ text: newMessage.value }));
    newMessage.value = '';
  }
  scrollToBottom()
}

const scrollToBottom = () => {
  setTimeout(()=>{
    let elem = document.querySelector("#main > div > div.chat-box .message-container:last-child")
    if (elem) elem.scrollIntoView({behavior: 'smooth'});
  },10)
}


onMounted(()=>{
  setupWebSocket();
})



</script>

<template>

  <main id="main">
    <div class="chat-box-container">
      <h1 class="chat-box-header"><img class="logo" src="/logo.png" /> <span class="logo-text">Privet.GE</span></h1>
      <div class="online__users"><span>{{onlineUsers}} Online</span></div>
      <div class="statusbar">
        <div class="left-status">
          <div class="status-container" :class="status"  v-if="status !== 'initial' ">
            <div class="dot"></div>
            <div class="text">{{ statusToText }}</div>
          </div>
        </div>
        <button class="skip" @click="setupWebSocket">Skip</button>
      </div>
      <div class="chat-box" ref="chatBox">
        <div v-if="status === 'waiting'" class="lds-ripple"><div></div><div></div></div>
        <div class="message-container" v-for="(message, index) in messages" :key="index">
          <div :class="message.class">
            <p>{{message.text}}</p>
          </div>
          <span :class="`${message.class}-date`">{{ message.date }}</span>
        </div>
      </div>
      <div v-if="typing" class="typing">Typing...</div>
      <div class="chat-input-container">
        <input class="chat-input" type="text" v-model="newMessage" @keyup.enter="sendMessage" @input="sendTyping">
        <button class="chat-submit" type="button" name="submit" @click="sendMessage" :disabled="!isConnected">SEND</button>
      </div>
    </div>

  </main>
</template>

<style scoped>

</style>