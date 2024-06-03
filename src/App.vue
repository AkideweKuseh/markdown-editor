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
        mainContent.classList.toggle('slide');
        header.classList.toggle('menu-active')
      },
      slidePreview(){
        const markdown = document.getElementById('text-container')!;
        const preview = document.getElementById('preview-box')!;
        const showIcon = document.getElementById('preview-markdown')!;
        const hiddenIcon = document.getElementById('preview-only')!;

        markdown.classList.toggle('hide-markdown');
        preview.classList.toggle('show-preview');
        showIcon.classList.toggle('hide-icon');
        hiddenIcon.classList.toggle('hide-icon')
      }
    }
  }
</script>

<template>
   <sidebar></sidebar>
   <editor @slide-action="slideSidebar" @slide-preview="slidePreview"></editor>
</template>

<style>
    .hidden {
      transform: translateX(-100%);
  }

    .slide {
      transform: translateX(250px);
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

    .show-preview{
    width: 100%;
  }

    .hide-markdown{
    width: 0;
  }

  .hide-icon{
    display: none;
  }
</style>
