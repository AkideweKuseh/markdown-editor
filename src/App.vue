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
        const Sidebar = document.getElementById('sidebar')!;
        const mainContent = document.getElementById('main-content')!;
        const header = document.getElementById('header')!;


        Sidebar.classList.toggle('hidden');
        mainContent.classList.toggle('full-width');
        header.classList.toggle('menu-active')
      }
    }
  }
</script>

<template>
   <sidebar></sidebar>
   <editor @slide-action="slideSidebar"></editor>
</template>

<style>
    .hidden {
      transform: translateX(-100%);
  }

    .full-width {
      margin-left: 0;
  }

     .menu-btn {
      display: block;
  }
  
    .menu-active .close-btn {
      display: block;
  }

    .menu-active .menu-btn{
      display: none;
    }

</style>
