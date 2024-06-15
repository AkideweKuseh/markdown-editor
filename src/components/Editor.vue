<template>
    <div class="main-content" id="main-content">
        <div class="header" id="header">
            <div class="header-left">
                <button class="menu-btn" @click="slideAction">
                    <img src="../assets/icon-menu.svg">
                </button>
                <button class="close-btn" @click="slideAction">
                    <img src="../assets/icon-close.svg">
                </button>
                <span class="logo"><img src="../assets/logo.svg"></span>
                <div class="document">
                        <div class="file-icon">
                            <img src="../assets/icon-document.svg" />
                        </div>
                    <div class="file-info">
                        <small>Document Name</small><br>
                        <span><input type="text" value="untitled-document.md"></span>
                    </div>
                </div>  
            </div>
            <div class="header-right">
                <img class="delete-icon" src="../assets/icon-delete.svg"/>
                <button class="btn-savemobile">
                    <img src="../assets/icon-save.svg"/>
                </button>
                <button class="btn-save">
                    <img class="save-icon" src="../assets/icon-save.svg"/>Save Changes
                </button>
            </div>
        </div>
        <div class="markdown-editor">
            <div class="text-container" id="text-container">
                <div class="inner-header">
                    <span>MARKDOWN</span>
                    <img src="../assets/icon-show-preview.svg" class="preview-mobile" @click="changePreview">
                </div>
                <textarea class="markdown" id="markdown" v-model="markdown">
                </textarea>
            </div>
            <div class="preview-box" id="preview-box">
                <div class="inner-header">
                    <span>PREVIEW</span>
                    <div class="preview-toggle">
                        <img src="../assets/icon-show-preview.svg" class="show-preview"
                        id="preview-markdown" 
                        @click="changePreview">
                        <img src="../assets/icon-hide-preview.svg" class="hide-preview hide-icon"
                        id="preview-only"
                        @click="changePreview">
                    </div>
                </div>
                <div class="preview" v-html="markdownToHtml"></div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
    import { marked } from 'marked'

    export default{
        name: 'Editor',
        data(){
            return{
                markdown: '',
            }
        },
        methods: {
            slideAction(){
                this.$emit('slideAction')
            },
            changePreview(){
                this.$emit('slide-preview')
            }
        },
        computed:{
            markdownToHtml(){
                return marked(this.markdown)
            }
        }
    }
</script>

<style>
    .inner-header .preview-toggle{
        display: flex;
        cursor: pointer;
    }

    .inner-header .preview-mobile{
        display: none;
    }
    .main-content {
        flex: 1;
        margin-left: 0px;
        transition: 0.5s ease-in-out;
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    .menu-btn, .close-btn {
        background: none;
        border: none;
        font-size: 24px;
        cursor: pointer;
        display: none;
        position: relative;
        left: 0;
    }

    .header {
        position: sticky;
        top: 0;
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: var(--headerBackgroundColor);
        padding: 20px 10px;
        width: 100%;
        color: var(--primaryColor);
        font-family: sans-serif;
        overflow: hidden;
    }

    .header-left{
        display: flex;
        align-items: center;
    }

    .header .logo{
        padding: 10px 30px;
        border-right: 1px solid var(--smallTextColor);
    }
/* Move media query code down */
    @media (max-width: 768px){
        .header .logo{
            display: none;
        }
        .header{
            width: 98%;
        }
    }

    @media (max-width: 446px){

        .markdown-editor .preview-box{
            width: 0;
        }

        .markdown-editor .text-container{
            width: 100%;
        }

        .header .header-right .btn-save{
            display: none;
        }

        .header .header-right .btn-savemobile{
            display: block;
        }

        .document .file-info br{
            display: none;
        }

        .document .file-info small{
            display: none;
        }

        .inner-header .preview-mobile{
            display: inline;
        }

        .header{
            width: 96%;
        }

        .preview{
            width: auto !important;
        }
    }

    .header-left .document{
        margin-left: 2rem;
    }

    .document .file-info small{
        color: var(--smallTextColor);
    }

    .document input{
        background: none;
        border: none;
        outline: none;
        color: var(--primaryColor);
        caret-color: var(--btnIdleColor);
    }

    .document input:focus{
        border-bottom: 1px solid var(--primaryColor);
    }

    .header-right{
        display: flex;
        align-items: center;
    }

    .header-right .btn-save{
        padding: 10px 16px;
        display: flex;
        align-items: center;
        margin: 0 1rem;
        border-radius: 5px;
        background: var(--btnIdleColor);
        border: none;
        color: var(--primaryColor);
        cursor: pointer;
    }

    .header-right .btn-save:hover{
        background: var(--btnHoverColor);
    }

    .header-right .btn-savemobile{
        display: none;
        padding: 5px;
        margin: 0 1rem;
        border-radius: 5px;
        background: var(--btnIdleColor);
        border: none;
        color: var(--primaryColor);
        cursor: pointer;
    }

    .header-right .save-icon{
        margin-right: 0.5rem;
    }

    .header-right .delete-icon:hover{
        filter: invert(50%) sepia(100%) saturate(400%) hue-rotate(-30deg);
        cursor: pointer;
    }

    .inner-header{
        display: flex;
        justify-content: space-between;
        position: sticky;
        top: 0;
        z-index: 1000;
        background: var(--innerHeaderBackgroundColor);
        color: var(--innerHeaderTextColor);
        padding: 10px 10px 10px 20px;
        font-family: Commissioner, sans-serif;
        letter-spacing: 4px;
        font-size: 13px;
    }

    .markdown-editor {
        position: static;
        display: flex;
        height: calc(88vh - 10px);
        color: var(--textColor);
        background: var(--primaryColor);
    }

    .text-container{
        position: relative;
        width: 50%;
        transition: all 0.5s ease;
        overflow-y: auto;
        color: var(--textColor);
        background: var(--primaryColor);
    }

    .text-container::-webkit-scrollbar {
            display: none; /* WebKit browsers */
        }

    .markdown {
        position: absolute;
        left: 0;
        right: 0;
        padding: 20px;
        border: none;
        resize: none;
        outline: none;
        font-size: 14px;
        height: 100%;
        overflow: hidden;
        color: var(--textColor);
        background: var(--primaryColor);
    }
    

    .preview-box {
        width: 50%;
        border-left: 1px solid #bdc3c7;
        transition: all 0.5s ease;
        z-index: 2;
        overflow-y: auto;
        color: var(--textColor);
        background: var(--primaryColor);
    }

    .preview-box::-webkit-scrollbar {
            display: none; /* WebKit browsers */
        }

    .preview-box .inner-header{
        display: flex;
        justify-content: space-between;
    }

    .preview{
        width: auto;
        height: 120%;
        padding: 20px;
        font-size: small;
        color: var(--textColor);
        background: var(--primaryColor);
        transition: all 1s ease;
    }
</style>