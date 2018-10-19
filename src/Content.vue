<template>
    <aside class="lg-side">
            <div class="inbox-head">
               
            </div>
             <h3> {{currentView.card-title}}</h3>
                 <keep-alive>
                        <component :is="currentView.tag"></component>
                </keep-alive>
         </aside>
</template>

<script>
import Inbox from './Inbox'
import Sent from './Sent'
import Important from './Important'
import Trash from './Trash'
import ViewMessage from './ViewMessage'
import { eventBus} from './main'

export default {
    
    created(){
        eventBus.$on('changeView', (data)=>{
            let temp =[{
                tag: data.tag, 
                title: data.title
            }];
            this.history = temp.concat(this.history.splice(0));
        })

    },
    data() {
        return {
            history: [
                {
                    tag: 'app-inbox',
                    title: 'Inbox'
                }
            ]
        };
    },
    computed: {
        currentView() {
            return this.history[0]
        }
    },
    components: {
        'app-inbox': Inbox,
        'app-sent': Sent,
        'app-Important': Important,
        'app-Trash': Trash,
        'app-view-message': ViewMessage

    }

}
</script>

<style>

</style>
