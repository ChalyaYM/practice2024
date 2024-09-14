<template>
    <div class="cont">
        <div class="search">
            <span class="search-title">Введите название блюда:</span><br>
            <input type="text" v-model="search_key" @keyup.enter="fetchRecipe" class="input">
            <button class="click-to-search" @click="fetchRecipe">Найти</button>
            <div v-if="!havingRecipes" class="substitution">
                <div v-if="!clickToSearch" class="notice">
                    Здесь отобразятся блюда после нажатия кнопки "Найти"
                </div>
                <div v-if="errOfSearch" class="not-found">
                    Ничего не найдено
                </div>
                <div v-if="isLoading" class="loading"> 
                    Идёт загрузка...
                </div>
            </div>
        </div>
        <div v-if="havingRecipes">
            <div v-if="clickToSearch&&!show" class="part-recipes">
                <ListOfRecipes v-bind:list="part_of_recipes"/>
                <MyButton @click="show_more" class="show-more">Показать еще</MyButton>
            </div>
            <div v-if="clickToSearch&&show" class="list-recipes">
                <ListOfRecipes v-bind:list="list_of_recipes"/>
            </div>
        </div>
    </div>
</template>

<script>
import ListOfRecipes from './ListOfRecipes.vue';
import MyButton from './MyButton.vue';

    export default {
        components: {
            ListOfRecipes, MyButton
        },
        data(){
            return {
                search_key: '',
                isLoading: false,
                havingRecipes: false,
                clickToSearch: false,
                errOfSearch: false,
                list_of_recipes: [],
                part_of_recipes: [],
                show: false,
            }
        },
        methods: {
            async fetchRecipe() {
                try {
                    this.errOfSearch = false;
                    this.havingRecipes = false;
                    this.clickToSearch = true;
                    this.isLoading = true;
                    this.show = false;
                    const param = this.search_key;
                    const response = await fetch(`https://api.edamam.com/api/recipes/v2?type=public&q=${param}&app_id=9bd947a6&app_key=69a3a8abbd86df181f6c6259ae8255aa`);
                    const result = await response.json();
                    if(!result.count) {
                        this.errOfSearch = true;
                    } else {
                        this.havingRecipes = true;
                        this.split_arr(result);
                    }
                    this.isLoading = false;
                } catch(e) {
                    alert('Ошибка');
                }
            },
            split_arr(result) {
                this.part_of_recipes = [];
                this.list_of_recipes = [];
                for (let i = 0; i < 3; i++) {
                    this.part_of_recipes.push(result.hits[i]);
                }
                for (let i = 0; i < result.hits.length; i++) {
                    this.list_of_recipes.push(result.hits[i]);
                }
            },
            show_more() {
                this.show = true;
            }
        }
    }
</script>

<style>
.cont {
    width: inherit;
}
.search {
    /* width: max-content; */
    text-align: center;
}

.search-title {
    font-size: 200%;
}

.input {
    margin-top: 20px;
    width: 300px;
    padding: 5px;
}

.click-to-search {
    width: 60px;
    margin-left: 20px;
    background-color: white;
    border: 1px solid black;
    padding: 5px;
    border-radius: 3px;
}

.substitution {
    height: 500px;
}

.notice {
    position: relative;
    top: 40%;
    font-size: larger;
    color: rgb(199, 199, 199);
}

.not-found, .loading {
    margin-top: 50px;
    font-size: larger;
}

.show-more {
    position: relative;
    left: 50%;
    top: 30px;
    transform: translate(-50%,0);
    background-color: white;
    border: none;
    border-bottom: 1px solid black;
    border-radius: 0;
    padding: 0 5px 0 5px;
}
</style>