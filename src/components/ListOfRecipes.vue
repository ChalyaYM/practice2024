<template>
    <div class="recipes" v-for="(val,index) in list">
        <ConcretRecipe v-bind:recipe="val.recipe"/>
    </div>
</template>

<script>
import ConcretRecipe from './ConcretRecipe.vue';

export default {
    components: {
        ConcretRecipe,
    },
    props: {
        list: {
            type: Array,
            required: true
        },
    },
}
</script>

<style>

</style>