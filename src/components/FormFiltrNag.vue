<template>
    <form class="courses-form form" id="filterform" role="form">
        <!-- Предметы -->
        <div>
            <select  id="subj" name="subject" @click="choiceValue">
                <template v-for="index in lessons">
                    <option >{{index}}</option>
                </template>
                
            </select>
        </div>

        <!-- Жанр курса -->
        <div>
            <select id="genre" name="genre" @click="choiceValue">
                <template v-for="genre in genres">
                    <option>{{genre}}</option>
                </template>
            </select>
        </div>

        <!-- Классы -->
        <div>
            <select id="grade" name="grade" @click="choiceValue">
                <option value="">Все классы</option>
                <template v-for="n in 11">
                    <option>{{n}}</option>
                </template>
                </select>
        </div>

        <!-- Поиск -->
        <div>
            <input class="borderFind" type="text" placeholder="Поиск" id="search" name="search" v-model="search ">
            <button class="courses-form-search-btn" type="button" title="Найти" @click="searchValue"></button>
        </div>
        <!-- {{objFilter}} -->
    </form>
</template>

<script>
export default {
    props: ['lessons', 'genres', 'objFilter'],
    data() {
        return {}
        
    },
    methods: {
        choiceValue(oe){
            if(oe.target.tagName != 'OPTION') return;
            this.objFilter[oe.currentTarget.name] = (
                oe.target.innerText == 'Все предметы' || 
                oe.target.innerText == 'Все классы' ||
                oe.target.innerText == 'Все жанры') ? '' : oe.target.innerText;

            if(this.objFilter.key == 1){
                this.objFilter.key = 2
            }else{
                this.objFilter.key = 1
            }
        },
        searchValue(oe){
            this.objFilter.search = oe.target.parentNode.children[0].value;
            if(oe.target.value) return
        }
    }
}
</script>

<style  lang="stylus">
    
</style>