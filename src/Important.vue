<template>
   <div class="inbox-body">
       <app-messages :messages="importantMessages"></app-messages>
   </div>
</template>

<script>
import Messages  from './Messages';
export default {
    props: {
        data: {
            type: Object,
            required: true
        }
    },
    computed: {
        importantMessages(){
            return this.data.messages.filter(function(messages){
                    return (messages.type == 'incoming' && messages.isImportant===true && !messages.isDeleted);
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
