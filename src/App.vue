<template>
    <BackImage class="back" id="back"/>
    <MainTitle class="main-title">
        <a href="#search"><MyButton class="scroll">Вперед!</MyButton></a>
    </MainTitle>
    
    <BackBlock class="ground">
        <SearchLine @search-recipes="recipe" class="search-food" id="search"/>
        <ListOfRecipes v-bind:list="list_of_recipes" v-bind:part="part_of_recipes" v-bind:show_flag="show_flag" class="recipes"/>
    </BackBlock>
    <Toolbar class="bar"><Logo @click="reload"/></Toolbar>
</template>

<script>
import Toolbar from "./components/Toolbar.vue";
import MainTitle from "./components/MainTitle.vue";
import BackImage from "./components/BackImage.vue";
import InfoTable from "./components/InfoTable.vue";
import BackBlock from "./components/BackBlock.vue";
import SearchLine from "./components/SearchLine.vue";
import ListOfRecipes from "./components/ListOfRecipes.vue";
import MyButton from "./components/MyButton.vue";
import Logo from "./components/Logo.vue";

export default {
    components: {
        Toolbar, MainTitle, BackImage, InfoTable, SearchLine, BackBlock, ListOfRecipes, MyButton, Logo
    },
    data() {
        return {
            list_of_recipes: [],
            part_of_recipes: [],
            count_of_recipes: 3,
            show_flag:false,
        }
    },
    methods: {
        recipe(result){
            this.list_of_recipes.length = 0;
            this.part_of_recipes.length = 0;
            for (let i = 0; i < this.count_of_recipes; i++) {
                this.part_of_recipes.push(result.hits[i]);
            }
            for (let i = this.count_of_recipes; i < result.hits.length; i++) {
                this.list_of_recipes.push(result.hits[i]);
            }
            console.log(this.list_of_recipes);
        },
        reload() {
            
            let elem = document.getElementById('back');
            elem.scrollIntoView(true);
            this.list_of_recipes = [];
            this.part_of_recipes = [];
            
        },
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    scroll-behavior: smooth;
}

body {
    background-color: rgb(162, 162, 162);
}

.bar {
    position: fixed;
}

.main-title {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translate(-50%, 0);
}

.back {
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
}

/* .info {
    position: relative;
    left: 20%;
    margin-top: 50px;
} */

.search-food {
    position: relative;
    left: 50%;
    transform: translate(-50%, 0);
    margin-top: 70px;
}

.ground {
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
    top: 100vh;
}

.scroll {
    width: 45%;
    height: 35px;
}
</style>