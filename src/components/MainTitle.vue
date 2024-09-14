<template>
    <div class="maintxt">
        <span class="welcome">Добро пожаловать</span><br>
        Опробуйте наш сервис прямо сейчас<br>
        <slot></slot>
    </div>
    
</template>

<script>

</script>

<style scoped>
.maintxt {
    width: fit-content;
    font-size: 250%;
    text-align: center;
    color: white;
}

.welcome {
    font-size: 160%;
}


</style>