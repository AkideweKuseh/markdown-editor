<template>
    <div class="popup" id="popup">
        <div class="popup-inner">
            <div class="close" @click="closeModal">&#10005;</div>
            <slot />
            <button @click="deleteFile">Confirm & Delete</button>
        </div>
    </div>
</template>

<script lang="ts">
    export default{
        name: 'Modal',
        methods: {
            closeModal(){
                this.$emit('closeModal')
            },
            deleteFile(){
                this.$emit('deleteFile')
            }
        }
    }

</script>

<style scoped>
    .popup{
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        z-index: 20000;
        background: rgba(45, 45, 45, 0.7);
    }

    .popup-inner{
        display: flex;
        flex-direction: column;
        justify-content: center;
        max-width: 280px;
        padding: 20px;
        border-radius: 5px;
        font-size: 14px;
        color: var(--textColor);
        background: var(--primaryColor);
    }

    button{
        padding: 10px;
        border-radius: 5px;
        margin-top: 1.5rem;
        background: var(--btnIdleColor);
        border: none;
        color: #ffffff;
        cursor: pointer;
    }

    .close{
        cursor: pointer;
        margin-bottom: 10px;
    }
</style>