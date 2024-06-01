<script lang="ts">
import Sidebar from '@/components/Sidebar.vue'
import Editor from '@/components/Editor.vue'
  export default{
    name: 'App',
    components: {
      Sidebar,
      Editor
    },
    data(){
      return{
        menuActive: false,
      }
    },
    methods: {
      slideSidebar(){
        
      }
    }
  }
</script>

<template>
   <sidebar></sidebar>
   <editor></editor>
</template>

<style>
  
</style>
