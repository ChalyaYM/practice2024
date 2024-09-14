<template>
    <div class="contein-info">
        <div class="circle"></div>
        <div class="text-info">
            <slot></slot>
        </div>
    </div>
</template>

<script>

</script>

<style scoped>
.contein-info {
    display: flex;
}

.circle {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: rgb(52, 52, 52);
    align-self: center;
}

.text-info {
    align-self: center;
    margin-left: 10px;
}
</style>