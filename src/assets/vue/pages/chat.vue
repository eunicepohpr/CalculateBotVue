<template id="page-chat">
    <f7-page>
      <f7-messages style="padding-bottom: 40px">
        <f7-message v-for="msg in messages" :name="msg.name" :text="msg.text" :type="msg.type"></f7-message>
      </f7-messages>
      <f7-messagebar placeholder="Message" send-link="Send" @submit="onSend"></f7-messagebar>
   </f7-page>
  </template>

<script>
var url = "https://calculatebotnode.au-syd.mybluemix.net/";
export default {
      data: function () {
        return {
          sessionId: (function(){
            var now = new Date();
            var enterDT = now.getFullYear() + now.getMonth() + now.getDate() + now.getTime()
            return enterDT;
          }()),
          messages: [{
            name:"Bot", 
            text:"Hello, I am Mathsbot do you want to add, subtract, divide or multiply?", 
            type:"received"
          }],
          context: {}
        }
      },
      methods: {
        onSend: function (text, clear) {
          console.log(this.sessionId)
          if (text.trim().length === 0) return;

          this.messages.push({
            name: "You",
            text: text,
            type: "sent"
          });

          var request = {
            "userMsg": text,
            "id": this.sessionId,
            "context": this.context
          }

          this.$http.post(url, request)
            .then(response => {
              //console.log(response.body);
              this.context = response.body.context;
              this.messages.push({
                name: "Bot",
                text: response.body.botMessage,
                type: "received"
            });
          });
          clear();
        }
      }
}
</script>