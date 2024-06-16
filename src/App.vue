<script lang="ts">
import Sidebar from '@/components/Sidebar.vue'
import Editor from '@/components/Editor.vue'
import Toggler from './components/Toggler.vue';
import data from '@/data.json'


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
        files: data
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
        const previewBox = document.getElementById('preview-box')!;
        const showIcon = document.getElementById('preview-markdown')!;
        const hiddenIcon = document.getElementById('preview-only')!;
        const preview = document.querySelector('.preview')!;

        markdown.classList.toggle('hide-markdown');
        previewBox.classList.toggle('show-preview');
        showIcon.classList.toggle('hide-icon');
        hiddenIcon.classList.toggle('hide-icon')
        preview.classList.toggle('resize-preview')
      },
      switchTheme(){
        //const toggleSwitch = document.getElementById('toggle-switch')!;
        const sunIcon = document.getElementById('sun')!;
        const moonIcon = document.getElementById('moon')!;
        const workSpace = document.querySelector('.markdown-editor')!;

        sunIcon.classList.toggle('active-theme');
        moonIcon.classList.toggle('active-theme');
        workSpace.classList.toggle('dark-theme');

        // toggleSwitch.addEventListener('change', (event) =>{
        //     if((<HTMLInputElement>event.target).checked){
        //         sunIcon.classList.remove('active-theme');
        //         moonIcon.classList.add('active-theme');

        //         workSpace.classList.add('dark-theme');
        //     }else{
        //         sunIcon.classList.add('active-theme');
        //         moonIcon.classList.remove('active-theme');

        //         workSpace.classList.remove('dark-theme');
        //     }
        // });

        // using localStorage to save theme state

        let theme;
        if(workSpace.classList.contains('dark-theme')){
            theme = 'DARK';
            //console.log('DARK')
        }else{
            theme = 'LIGHT'
            //console.log('LIGHT')
        }

        localStorage.setItem('theme', JSON.stringify(theme));

      }
    }
  }
</script>

<template>
   <sidebar @change-theme="switchTheme" :files="files"></sidebar>
   <editor @slide-action="slideSidebar" @slide-preview="slidePreview" :files="files"></editor>
</template>

<style>
  .resize-preview{
    width: 50%;
    margin: 0 auto;
  }

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
    width: 100% !important;
  }

    .hide-markdown{
    width: 0 !important;
  }

  .hide-icon{
    display: none;
  }
</style>
