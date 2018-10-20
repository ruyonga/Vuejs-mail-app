<template>
    <aside class="sm-side">
        <div class="user-head">
            <img src="src/assets/logo.png" width="30px" height="30px" />

            <div class="user-name">
                <h5>Bo Andersen</h5>
                <span class="email-address">info@codingexplained.com</span>
            </div>
        </div>

        <div class="compose-wrapper">
            <app-compose></app-compose>
        </div>

        <ul class="inbox-nav">
            <li :class="{ active: activeView == 'app-inbox' }">
                <a href="#" @click.prevent="navigate('app-inbox', 'Inbox')">
                    <i class="fa fa-inbox"></i>Inbox <span class="label label-danger pull-right">{{ unreadMessages.length }}</span>
                </a>
            </li>

            <li :class="{ active: activeView == 'app-sent' }">
                <a href="#" @click.prevent="navigate('app-sent', 'Sent')">
                    <i class="fa fa-envelope-o"></i>Sent <span class="label label-default pull-right">{{ sentMessages.length }}</span>
                </a>
            </li>

            <li :class="{ active: activeView == 'app-important' }">
                <a href="#" @click.prevent="navigate('app-important', 'Important')">
                    <i class="fa fa-bookmark-o"></i>Important <span class="label label-warning pull-right">{{ importantMessages.length }}</span>
                </a>
            </li>

            <li :class="{ active: activeView == 'app-trash' }">
                <a href="#" @click.prevent="navigate('app-trash', 'Trash')">
                    <i class=" fa fa-trash-o"></i>Trash <span class="label label-default pull-right">{{ trashedMessages.length }}</span>
                </a>
            </li>
        </ul>
    </aside>
</template>
<script>

import { eventBus } from './main'
import Compose from './Compose'
// Event bus handles communication between oncomponets based on events
// eventBus.$emit => sends events
// eventBus.$on('method', (data)=>{}) receives

export default {
    props: {
        messages: {
            type: Array,
            required: true
        }
    },
    created() {
        eventBus.$on('changeView', (data) => {
            this.activeView == data.tag
        });
    },

    data() {
        return {
                activeView: 'app-inbox'
             }
    },

    methods: {
        navigate(newView, title){
            eventBus.$emit('changeView',{
                tag: newView,
                title: title
      });
    }
    },
    computed: {
        unreadMessages(){
            return this.messages.filter(function(messages){
                    return (messages.type == 'incoming' && !messages.isRead && !messages.isDeleted);
            });
        },
        sentMessages(){
            return this.messages.filter(function(messages){
                    return (messages.type == 'outgoing' && !messages.isDeleted);
            });
        },  
       importantMessages(){
            return this.messages.filter(function(messages){
                    return (messages.type == 'incoming' && messages.isImportant===true && !messages.isDeleted);
            });
       },
        trashedMessages(){
            return this.messages.filter(function(messages){
                    return messages.isDeleted === true;
            });
        }
        

    },
    components: {
        'app-compose': Compose
    }
 
}


</script>

<style>

</style>
 