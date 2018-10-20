<template>
<div>
    <table v-if="messages.length > 0" class="table table-inbox table-hover">
        <tbody>
            <tr @click="openMessage(message)" v-for="(message, key) in messages" :key="key" :class="{unread: typeof message.isRead !== 'undefined' && !message.isRead }" >
                <td><input type="checkbox" name="" id=""></td>
                <td>
                    <a href="#" v-if="typeof message.isImportant !== undefined" @click.prevent.stop="messages.isImportant=!message.isImportant">
                        <i :class="['fa', 'fa-star', { isImportant: message.isImportant }]"></i>
                    </a>
                </td>
                <td>{{ message.from.name}}</td>
                <td>{{message.subject}}</td>
                <td><i v-if="message.attachments.length >0" class="fa fa-paperclip"></i></td>
                <td class="text-right">{{ message.date.fromNow()}}</td>
            </tr>
        </tbody>
    </table>
<p v-else >No Messages here yer</p>
</div>
</template>

<script>
import { eventBus } from './main'
export default {
    props: {
        messages: {
            type: Array,
            required: true
        }
    },
    methods: {
        openMessage(message){
            eventBus.$emit('changeView', {
                tag: 'app-view-message',
                title: message.subject,
                data: {
                    message: message
                }
            });
        }
    }

}
</script>

<style>

</style>
