<script lang="ts">
import Sidebar from '@/components/Sidebar.vue'
import Editor from '@/components/Editor.vue'
import Toggler from './components/Toggler.vue';
import Modal from './components/Modal.vue';
import data from '@/data.json'

interface File {
        createdAt: string;
        name: string;
        content: string;
    }

  export default{
    name: 'App',
    components: {
      Modal,
      Sidebar, 
      Editor,
      Toggler,
    },
    mounted(){
      let getTheme = window.localStorage.theme 
          if(JSON.parse(getTheme) === 'DARK'){
              const checkBox = document.getElementById('toggle-switch') as HTMLInputElement;
              checkBox.checked = true
              this.switchTheme();
          }
    },
    data(){
      return{
        menuActive: false,
        files: data,
        selectedFileContent: 'x',
        deleteFile: false,
        fileToDelete: '',
        theme: ''
      }
    },
    // watch: {
    //   theme(newValue, oldValue){
        
    //   }
    // },
    methods: {
      displayFile(file: File){
        this.selectedFileContent = file.content;

        const fileName = document.getElementById('file-name') as HTMLInputElement;
        fileName.value = file.name
      },
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
        const sunIcon = document.getElementById('sun')!;
        const moonIcon = document.getElementById('moon')!;
        const workSpace = document.querySelector('.markdown-editor')!;
        const modal = document.getElementById('popup')!;

        sunIcon.classList.toggle('active-theme');
        moonIcon.classList.toggle('active-theme');
        workSpace.classList.toggle('dark-theme');
        modal.classList.toggle('dark-theme');
 
        if(workSpace.classList.contains('dark-theme')){
            this.theme = 'DARK';
        }else{
            this.theme = 'LIGHT'
        }

        localStorage.setItem('theme', JSON.stringify(this.theme));

      },
      deleteItem(){
        this.deleteFile = true;

        const fileName = document.getElementById('file-name') as HTMLInputElement;

        this.fileToDelete = fileName.value
      },
      exitModal(){
        this.deleteFile = false;
      },
      createNewFile(){
        //const activeMarkdown = document.getElementById('markdown') as HTMLTextAreaElement;
        const fileName = document.getElementById('file-name') as HTMLInputElement;
        const newFile: File = {...this.files[0]};

        this.files.unshift(newFile);
        this.selectedFileContent = newFile.content;
        //activeMarkdown.focus();
        fileName.value = newFile.name;
      }
    }
  }
</script>

<template>
   <sidebar @change-theme="switchTheme" @newFile="createNewFile" :files="files" @fileSelected="displayFile($event)"></sidebar>
   <editor 
   @slide-action="slideSidebar" 
   @slide-preview="slidePreview"
   @delete-document="deleteItem" 
   :files="files"
   :selectedFileContent="selectedFileContent">
   </editor>
   <modal v-show="deleteFile" @close-modal="exitModal">
    <h5>Delete Document?</h5>
    <p>Are you sure want to delete the <br>
    {{ fileToDelete }} document and its Content?<br>
    This action can not be reversed.
  </p>
   </modal>
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
