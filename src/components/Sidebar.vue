<template>
    <div class="sidebar hidden" id="sidebar">
        <div class="sidebar-header">
            <div class="logo"><img src="../assets/logo.svg"></div>
            <span>MY DOCUMENTS</span>
        </div>
        <div class="sidebar-content">
            <button class="btn">+ New Document</button>
            <ul class="documents">
                <li v-for="file in files" :key="file.name">
                    <div class="document">
                        <div class="file-icon">
                            <img src="../assets/icon-document.svg" />
                        </div>
                    <div class="file-info">
                        <small>{{ file.createdAt }}</small><br><span>{{ file.name }}</span>
                    </div>
                    </div>  
                </li>
            </ul>
            <div class="toggler">
                <img src="../assets/icon-dark-mode.svg" id="moon" />
                <toggler @change-theme="changeTheme"></toggler>
                <img class="active-theme" id="sun" src="../assets/icon-light-mode.svg" />
            </div>
        </div>
    </div>
</template>

<script  lang="ts">
    import type { PropType } from 'vue';
    import Toggler from './Toggler.vue'

    interface File {
        createdAt: string;
        name: string;
        content: string;
    }

    export default{
        name: 'Sidebar',
        props: {
            files: {
                type: Array as PropType<File[]>,
                required: true
            }
        },
        components: {
            Toggler
        },
        methods: {
            changeTheme(){
                this.$emit('changeTheme')
            }
        }
    }
</script>

<style>
    .sidebar {
        width: 219px;
        background: var(--sidebarColor);
        color: white;
        position: fixed;
        top: 0;
        left: 0;
        min-height: 100vh;
        padding: 1rem;
        transition: transform 0.5s ease-in-out;
        transform: translateX(0);
        font-family: sans-serif;
    }

    .sidebar .sidebar-header{
        margin-top: 0.5rem;
        color: var(--smallTextColor);
    }

    .btn{
        padding: 10px;
        border-radius: 5px;
        width: 90%;
        margin-top: 1.5rem;
        background: var(--btnIdleColor);
        border: none;
        color: var(--primaryColor);
        cursor: pointer;
    }

    .btn:hover{
        background: var(--btnHoverColor);
    }

    .documents {
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .documents li {
        padding: 10px 0;
    }

    .documents li small{
        color: var(--smallTextColor);
    }

    .document{
        display: flex;
        align-items: center;
    }

    .document .file-icon{
        margin-right: 0.8rem;
    }

    .toggler{
        position: fixed;
        bottom: 50px;
        left: 30px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .toggler button{
        margin: 0 5px;
    }

    .active-theme{
        filter: invert(100%) brightness(1000%);
    }

    .sidebar-header .logo{
        margin-bottom: 1rem;
        display: none;
    }

    @media (max-width: 768px){
        .sidebar-header .logo{
        display: block;
    }
    }
</style>