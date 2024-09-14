<template>
<div class="dialog" v-if="show" @click="hideDialog">
    <div @click.stop class="dialog-content">
        <slot></slot>
    </div>
</div>
</template>

<script>
export default {
    props: {
        show: {
            type: Boolean,
            default: false,
        }
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false);
        }
    }
}
</script>

<style scoped>
.dialog {
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0,0,0, 0.5);
    position: fixed;
    display: flex;
    z-index: 30;
    /* width: 100%;
    height: 100vh; */
}

.dialog-content {
    margin:auto;
    border-radius: 12px;
    background-color: white;
    padding: 35px;
    width: max-content;
    min-width: 500px;
    min-height: 350px;
    /* align-self: flex-start; */
}
</style>