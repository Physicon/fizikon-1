<template>
    <div class="list_books_nag">
        <form>
            <h2>Показывать стоимость в:</h2>
            <label for="rub">
                <input type="radio" name="prise" id="rub" checked v-model="isPrice" :value='true' @input="changeKey"> <span>рублях</span>
            </label>
            <label for="bonus">
                <input type="radio" name="prise" id="bonus" v-model="isPrice" :value='false' @input="changeKey"> <span>бонусах</span>
            </label>
        </form>
        
        <ul class="courses-list" id="courseslist" :key="myKey">
            <template  v-for="cours in courses">
                <template
                    v-if='
                        (
                            objFilter.subject  == ""
                            || objFilter.subject == cours.subject
                        )&&(
                            objFilter.grade == ""
                            || filterGrade(objFilter, cours) 
                        )&&(
                            objFilter.genre == ""
                            || objFilter.genre == cours.genre
                        )&&(
                            objFilter.search == ""
                            || filterSearch(objFilter, cours)
                        )'
                >
                    <li class="courses-sci">
                        <div class="sci-figure">
                            <img :src="cours.imgSrc" :alt="cours.genre">
                        </div>
                        <div class="sci-info">
                            <p class="sci-title">{{cours.subject}}</p>
                            <p class="sci-title" :title="cours.title">{{cours.title}}</p>
                            <p class="sci-grade">{{stringGrade(cours)}} класс</p>
                            <p class="sci-genre">{{cours.genre}}</p>
                            <p class="sci-meta"><a :href="cours.shopUrl" target="_blank">Подробнее</a></p>
                            <p class="sci-controls pure-button pure-button-primary btn-fluid">{{ isPrice ? cours.price + ' руб.' : cours.priceBonus + ' бонусов'}}</p>
                            <!-- {{cours}}}                 -->
                        </div>
                    </li>
                </template>
                
            </template>
        </ul>
    </div>
    
</template>

<script>
export default {
    props: ['courses', 'objFilter'],  
    data()  {
        return {
            isPrice: true,
            myKey: 1,
        }
    },

    methods: {

        stringGrade(course) {
            if(course.grade.length > 1){
                return course.grade.join(', ')                
            }else{
                return course.grade[0];
            }
        },
        filterGrade(objFilter, cours){
            for(var i = 0; i < cours.grade.length; i++){
                if(cours.grade[i] == objFilter.grade){
                    return true;
                }
            }
            return false;
        },
        filterSearch(objFilter, cours) {
            var stringSearch = cours.title.toLowerCase()
            if( stringSearch.indexOf(objFilter.search) >= 0){
                return true;
            } else {
                return false
            }
        },
        changeKey() {
            if(this.isPrice){
                this.myKey = 2;
            }else{
                this.myKey = 1;
            }
        }
    }
}
</script>

<style>
    .list_books_nag form {
        display: flex;
        align-items: baseline;
        padding: 0 15px;
    }
    .list_books_nag h2, .list_books_nag label{
        margin: 0;
        padding: 0;
        margin-right: 35px;
        font-family: "Segoe UI", "Helvetica Neue", Arial, serif;
        font-weight: normal;
        
    }
    .list_books_nag input {
        margin-right: 10px;
    }
    .sci-controls {
    margin-bottom: 0;
    padding-left: 0;
    font-size: 12px;
    background: rgb(0, 187, 235);
border-radius: 5px;
}
</style>