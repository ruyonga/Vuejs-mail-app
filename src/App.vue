<template>
 <div class="container">
   <div class="mail-box">
     <app-sidebar></app-sidebar>
     <app-content></app-content>
   </div>
 </div>
</template>

<script>
import Sidebar from './Sidebar';
import Content from './Content';

export default {
  components: {
    'app-sidebar': Sidebar,
    'app-content': Content,
  }
}
</script>
