<template>
  <div class="chat-container">
    <div class="messages">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        :class="['message', msg.sender]"
      >
        {{ msg.text }}
      </div>
    </div>

    <div class="input-area">
      <input
        v-model="newMessage"
        @keyup.enter="sendMessage"
        type="text"
        placeholder="پیام خود را بنویسید..."
      />
      <button @click="sendMessage">ارسال</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatBox",
  data() {
    return {
      newMessage: "",
      messages: []
    };
  },
  methods: {
    sendMessage() {
      if (!this.newMessage.trim()) return;

    
      this.messages.push({
        text: this.newMessage,
        sender: "user"
      });

      this.newMessage = "";


      setTimeout(() => {
        this.messages.push({
          text: "پیام شما دریافت شد.",
          sender: "system"
        });
      }, 500);
    }
  }
};
</script>

<style>
.chat-container {
  width: 350px;
  border: 1px solid #ddd;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  font-family: sans-serif;
}

.messages {
  flex: 1;
  padding: 10px;
  overflow-y: auto;
  background: #f9f9f9;
}

.message {
  margin-bottom: 8px;
  padding: 6px 10px;
  border-radius: 6px;
  max-width: 80%;
  font-size: 14px;
}

.message.user {
  background: #d1e7ff;
  align-self: flex-end;
}

.message.system {
  background: #eaeaea;
  align-self: flex-start;
}

.input-area {
  display: flex;
  border-top: 1px solid #ddd;
}

.input-area input {
  flex: 1;
  border: none;
  padding: 10px;
  font-size: 14px;
  outline: none;
}

.input-area button {
  border: none;
  padding: 0 16px;
  cursor: pointer;
  background: #0d6efd;
  color: white;
  font-size: 14px;
}

.input-area button:hover {
  background: #0b5ed7;
}
</style>
