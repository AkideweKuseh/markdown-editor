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
                        <small>01 April 2022</small><br>
                        <span><input type="text" value="untitled-document.md"></span>
                    </div>
                    </div>  
            </div>
            <div class="header-right">
                <img class="delete-icon" src="../assets/icon-delete.svg"/>
                <button class="btn-save"><img class="save-icon" src="../assets/icon-save.svg"/>Save Changes</button>
            </div>
        </div>
        <div class="markdown-editor">
            <textarea class="markdown" id="markdown" v-model="markdown">
            </textarea>
            <div class="preview" id="preview">{{ markdown }}</div>
        </div>
    </div>
</template>

<script lang="ts">
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
            }
        }
    }
</script>

<style>
    .main-content {
        flex: 1;
        margin-left: 0px;
        transition: 0.5s ease-in-out;
        display: flex;
        flex-direction: column;
        height: 100vh;
        min-width: 100wv;
        padding: auto;
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

    /* .close-btn:hover {
        background: var(--navIconBacroundColor);
    } */

    /* .close-btn {
        display: block;
    }

    .menu-active .menu-btn {
         display: none;
    }

    .menu-active .close-btn {
        display: block;
    } */

    .header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: var(--headerBackgroundColor);
        padding: 10px;
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

    .header-right .save-icon{
        margin-right: 0.5rem;
    }

    .markdown-editor {
        display: flex;
        height: calc(100vh - 50px);
        color: var(--textColor);
    }

    .markdown {
        width: 50%;
        padding: 10px;
        border: none;
        resize: none;
        outline: none;
        font-size: 16px;
    }

    .preview {
        width: 50%;
        padding: 10px;
        overflow-y: auto;
        border-left: 1px solid #bdc3c7;
    }

</style>