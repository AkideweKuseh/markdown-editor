<template>
    <div class="popup">
        <div class="popup-inner">
            <span class="close">&#10005;</span>
            <slot />
            <button>Confirm & Delete</button>
        </div>
    </div>
</template>

<script lang="ts">
    export default{
        name: 'Modal',
    }

</script>

<style>
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
        z-index: 2000;
        background: rgba(0, 0, 0, 0.4);
    }

    .popup-inner{
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 20px;
        border-radius: 5px;
        color: var(--textColor);
        background: var(--primaryColor);
    }

    button{
        padding: 10px;
        border-radius: 5px;
        margin-top: 1.5rem;
        background: var(--btnIdleColor);
        border: none;
        color: var(--primaryColor);
        cursor: pointer;
    }

    .close{
        margin-right: 0;
        cursor: pointer;
    }
</style>