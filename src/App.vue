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

    const activeMarkdown = document.getElementById('markdown') as HTMLTextAreaElement;
    const fileName = document.getElementById('file-name') as HTMLInputElement;

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

      let getSidebarStatus = window.localStorage.sidebarStatus
          if(JSON.parse(getSidebarStatus) === 'ACTIVE'){
            this.slideSidebar()
          }
      let getFiles = JSON.parse(window.localStorage.Files);

      this.files = getFiles;
    },
    data(){
      return{
        menuActive: false,
        files: data,
        selectedFileContent: 'x',
        deleteFile: false,
        fileToDelete: '',
        theme: '',
        newFile:{
          createdAt: '04-01-2022',
          name: 'untitled-document.md',
          content: ''
        }
      }
    },
    // watch: {
    //   files(newValue, oldValue){
        
    //   }
    // },
    methods: {
      displayFile(file: File){
        const fileName = document.getElementById('file-name') as HTMLInputElement;

        this.selectedFileContent = file.content;
        fileName.value = file.name
      },
      slideSidebar(){
        const sidebar = document.getElementById('sidebar')!;
        const mainContent = document.getElementById('main-content')!;
        const header = document.getElementById('header')!;


        sidebar.classList.toggle('hidden');
        mainContent.classList.toggle('slide');
        header.classList.toggle('menu-active');

        let sidebarStatus ='';
        if(sidebar.classList.contains('hidden')){
            sidebarStatus = 'INACTIVE';
        }else{
            sidebarStatus = 'ACTIVE'
        }

        localStorage.setItem('sidebarStatus', JSON.stringify(sidebarStatus));
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
        const fileName = document.getElementById('file-name') as HTMLInputElement;
        const newFile: File = {...this.newFile};

        //this.files.unshift(newFile);
        this.selectedFileContent = newFile.content;
        
        fileName.value = newFile.name;
      },
      saveFile(){

          const activeMarkdown = document.getElementById('markdown') as HTMLTextAreaElement;
          const fileName = document.getElementById('file-name') as HTMLInputElement;

          const fileToSave: File = {...this.newFile}

          fileToSave.content = activeMarkdown.value
          fileToSave.name = fileName.value
          this.files.unshift(fileToSave)

          localStorage.setItem('Files', JSON.stringify(this.files));

          prompt(`${fileName.value} Saved!`)
      },
      deleteFileNow(){
        const activeMarkdown = document.getElementById('markdown') as HTMLTextAreaElement;
        const fileName = document.getElementById('file-name') as HTMLInputElement;

        for(let i = 0; i<this.files.length; i++){
            if(this.files[i].name === this.fileToDelete){
                this.files.splice(i, 1);
                //console.log(this.files[i].name, ' Deteted')
            }
          }
          localStorage.setItem('Files', JSON.stringify(this.files));
          this.exitModal()
          activeMarkdown.value = '';
          fileName.value = ''
          prompt(`${this.fileToDelete} Deleted!`)
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
   @save="saveFile" 
   :files="files"
   :selectedFileContent="selectedFileContent">
   </editor>
   <modal v-show="deleteFile" @close-modal="exitModal" @delete-file="deleteFileNow">
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
