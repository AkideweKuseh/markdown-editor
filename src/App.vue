<script lang="ts">
import Sidebar from '@/components/Sidebar.vue'
import Editor from '@/components/Editor.vue'
import Toggler from './components/Toggler.vue';
  export default{
    name: 'App',
    components: {
      Sidebar,
      Editor,
      Toggler
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
      },
      switchTheme(){
        const toggleSwitch = document.getElementById('toggle-switch')!;
        const sunIcon = document.getElementById('sun')!;
        const moonIcon = document.getElementById('moon')!;
        const workSpace = document.querySelector('.markdown-editor')!;

        toggleSwitch.addEventListener('change', (event) =>{
            if((<HTMLInputElement>event.target).checked){
                sunIcon.classList.remove('active-theme');
                moonIcon.classList.add('active-theme');

                workSpace.classList.add('dark-theme');
            }else{
                sunIcon.classList.add('active-theme');
                moonIcon.classList.remove('active-theme');

                workSpace.classList.remove('dark-theme');
            }
        });
      }
    }
  }
</script>

<template>
   <sidebar @change-theme="switchTheme"></sidebar>
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
