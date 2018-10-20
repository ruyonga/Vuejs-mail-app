<template>
   <div class="inbox-body">
       <app-messages :messages="sentMessages"></app-messages>
   </div>
</template>

<script>
import Messages from './Messages';
export default {
    props: {
        data: {
            type: Object,
            required: true
        }
    },
    computed: {
        sentMessages(){
            return this.data.messages.filter(function(messages){
                    return (messages.type == 'outgoing' && !messages.isDeleted);
            });
        }, 
    },
    components: {
        'app-messages': Messages
    }

}
</script>

<style>

</style>
