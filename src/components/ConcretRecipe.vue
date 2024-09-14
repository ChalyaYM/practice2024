<template>
    <div class="rec">
        <div class="icon">
            <img :src="recipe.image" alt="Изображение блюда" width="130px" height="130px">
        </div>
        <div class="description">
            <div class="title">{{ recipe.label }}</div>
            <hr>
            <div class="type">{{ recipe.mealType[0] }}</div>
            <MyButton class="show-recipe-dialog" @click="show_dialog">Показать полностью</MyButton>
            <Teleport to="body">
                <Dialog v-model:show="dialogVisible">
                    
                    <div class="title">{{ recipe.label }}</div>
                    <hr>
                    <div class="recipe-contain">
                        <div class="icon">
                            <img :src="recipe.image" alt="Изображение блюда" width="190px" height="190px">
                        </div>
                        <div class="text-recipe">
                            <div class="type">{{ recipe.mealType[0] }}</div>
                            <hr class="sub">
                            <div class="calories">{{ recipe.calories }} calories</div>
                            <hr class="sub">
                            <ul>
                                <div>Ingredients:</div>
                                <hr class="sub">
                                <div class="ingredients" v-for="val in recipe.ingredients">
                                    <li><div class="concret-ingr">{{ val.text }}</div></li>
                                    <hr class="sub">
                                </div>
                            </ul>
                        </div>
                    </div>
                </Dialog>
            </Teleport>
        </div>
        
    </div>
</template>

<script>
import Dialog from './Dialog.vue';
import MyButton from './MyButton.vue';

export default {
    components: {
        Dialog, MyButton
    },
    data() {
        return {
            dialogVisible: false,
        }
    },
    props: {
        recipe: {
            type: Object,
            required: true,
        },
        show: {
            type: Boolean
        }
    },
    methods: {
        show_dialog() {
            this.dialogVisible = true;
        }
    }
}
</script>

<style>
.rec {
    display: flex;
    position: relative;
    /* left: 15%; */
    margin-top: 30px;
}

.icon {
    margin-right: 15px;
}

img {
    box-shadow: 5px 4px 5px rgb(183, 183, 183);
    border-radius: 3px;
}

.title {
    font-size: 150%;
}

.description {
    height: inherit;
}

.show-recipe-dialog {
    padding: 3px;
    position: absolute;
    top: 100px;
}

.ingredients {
    margin-left: 20px;
}

.sub {
    border-top: 1px dashed rgb(221, 221, 221);
}

.recipe-contain {
    display: flex;
    margin-top: 20px;
}
</style>