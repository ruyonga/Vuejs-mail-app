<template>
   <div class="inbox-body">
                   <div class="mail-option">
                        <div class="btn-group">
           <a href="#" class="btn" @click="refresh">
               <i class="fa fa-refresh"></i>&nbsp; Refresh
           </a>
       </div>
                   </div>

      
       <app-messages :messages="incomingMessages"></app-messages>
   </div>
</template>

<script>
import Messages from './Messages';
import {eventBus} from './main';

export default {
        props: {
            data: {
                type: Object,
                required: true
            }
        },
        computed: {
            incomingMessages(){
                return this.data.messages.filter(function(messages){
                        return (messages.type == 'incoming'  && !messages.isDeleted);
                });
             },
        },
        components: {
                'app-messages': Messages
        },
        methods:{
                refresh(){
                    eventBus.$emit('refreshMessages');
                }
        }

}
</script>

<style>

</style>
