<template>
 <div class="container">
   <div class="mail-box">
     <app-sidebar :messages="messages"></app-sidebar>
     <app-content :messages="messages"></app-content>
   </div>
 </div>
</template>

<script>
import Sidebar from './Sidebar';
import Content from './Content';
import messages from './data/messages';
import randomMessages from './data/random-messages'
import {eventBus} from './main'

export default {

  data() {
    return {
      messages: messages
    };
  },
  created(){
    eventBus.$on('refreshMessages', ()=>{
        let randomeIndex = Math.floor(Math.random() * randomMessages.length);
        let temp = [randomMessages[randomeIndex]];
        this.messages = temp.concat(this.messages.slice(0));
    });

    eventBus.$on('sentMessage', (data)=>{
        let temp = [data.message];
        this.messages.temp.concat(this.messages.slice(0));
    })
  },
  components: {
    'app-sidebar': Sidebar,
    'app-content': Content
  }
}
</script>
