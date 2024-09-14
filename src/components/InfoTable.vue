<template>
    <div class="list">
        <div class="list-title">Почему именно мы?</div>
        <InfoText class="line">Простой и понятный интерфейс</InfoText>
        <InfoText class="line">Нужный рецепт всего в одном клике</InfoText>
        <InfoText class="line">Какой-то текст</InfoText>
    </div>
</template>


<script>
    import InfoText from "./InfoText.vue";

    export default {
        components: {
            InfoText
        }
    }
</script>

<style scoped>
.list {
    width: max-content;
}

.list-title {
    font-size: 250%;
    margin-bottom: 30px;
    text-align: center;
}

.line {
    margin-bottom: 30px;
    font-size: 150%;
}
</style>