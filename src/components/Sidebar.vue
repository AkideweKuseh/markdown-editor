<template>
    <div class="sidebar hidden" id="sidebar">
        <div class="sidebar-header">
            <span>MY DOCUMENTS</span>
        </div>
        <div class="sidebar-content">
            <button class="btn">+ New Document</button>
            <ul class="documents">
                <li>
                    <div class="document">
                        <div class="file-icon">
                            <img src="../assets/icon-document.svg" />
                        </div>
                    <div class="file-info">
                        <small>01 April 2022</small><br><span>untitled-document.md</span>
                    </div>
                    </div>  
                </li>
                <li>
                    <div class="document">
                        <div class="file-icon">
                            <img src="../assets/icon-document.svg" />
                        </div>
                    <div class="file-info">
                        <small>01 April 2022</small><br><span>untitled-document.md</span>
                    </div>
                    </div>  
                </li>
            </ul>
            <div class="toggler">
                <img src="../assets/icon-dark-mode.svg" />
                <toggler></toggler>
                <img src="../assets/icon-light-mode.svg" />
            </div>
        </div>
    </div>
</template>

<script  lang="ts">
    import Toggler from './Toggler.vue'
    export default{
        name: 'Sidebar',
        components: {
            Toggler
        }
    }
</script>

<style>
    .sidebar {
        width: 250px;
        background: var(--sidebarColor);
        color: white;
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
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
        bottom: 10px;
        left: 20px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .toggler button{
        margin: 0 5px;
    }
</style>