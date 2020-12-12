<template>
  <div class="content">
    <HeaderNag></HeaderNag>
    <div class="l-container-4">
      
      <h1 class="u-text-center">Витрина</h1>
      <div class="courses u-mt-30">
          <FormFiltrNag 
            :lessons = lessons
            :genres = genres
            :objFilter = objFilter
          />
          <ListBooksNag 
            :courses = courses
            :objFilter = objFilter
          />      
    </div>
    </div>    
  </div>
</template>

<script>
import HeaderNag from "./components/HeaderNag";
import FormFiltrNag from "./components/FormFiltrNag"
import ListBooksNag from "./components/ListBooksNag"

var ajax = new XMLHttpRequest();
ajax.open('POST', 'https://krapipl.imumk.ru:8443/api/mobilev1/update', false);
var fd = new FormData();
ajax.send(fd);
var objCourses = JSON.parse(ajax.responseText)
var coursesOriginal = objCourses.items


export default {
  name: 'App',
  components: {
    HeaderNag,
    FormFiltrNag,
    ListBooksNag,
  },
  data(){
    return {      
        objFilter: {
          key: 1,
          subject: '',
          grade: '',
          genre: '',
          search: ''
        }
    }
  },
  computed: {
    lessons(){ 
      var checkObjCourse = {};
      var lessonsArray = [];
      for(let i = 0; i < coursesOriginal.length; i++){
        var course = coursesOriginal[i];
        if(checkObjCourse[course.subject] == course.subject) continue;
        checkObjCourse[course.subject] = course.subject;
        lessonsArray.push(course.subject)
      }
      lessonsArray.unshift('Все предметы');
      return lessonsArray
    },
    genres(){
      var checkObjCourse = {};
      var lessonsArray = [];
      for(let i = 0; i < coursesOriginal.length; i++){
        var course = coursesOriginal[i];
        if(checkObjCourse[course.genre ] == course.genre ) continue;
        checkObjCourse[course.genre ] = course.genre ;
        lessonsArray.push(course.genre )
      }
      lessonsArray.unshift('Все жанры');
      return lessonsArray
    },
    courses() {
      for(let i = 0; i < coursesOriginal.length; i++) {
        var course = coursesOriginal[i];
        course.imgSrc = "https://www.imumk.ru/svc/coursecover/" + course.courseId;
        course.grade = course.grade.split(';');
      }
      return coursesOriginal;
    } 
  },  
}
</script>

<style>
html, body {
    height: 100%;
}
.wrapper {
    display: flex;
    flex-direction: column;
    height: 100%;
    margin: 0 auto;
    overflow: auto;
}
html, button, input, select, textarea, .pure-g [class*="pure-u"] {
  font-family: "Segoe UI", "Helvetica Neue", Arial, sans-serif; }
</style>
