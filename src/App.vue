<template>
  <div id="app">
    <div class="canvas-component">
      <canvasComp></canvasComp>
    </div>
    <div class="task-component">
      <task :exId="IdExercise"></task>
    </div>
    <footer>
      <div class="answers-component">
        <answers :exId="IdExercise" :doneList="done"></answers>
      </div>
      <div class="about">
        <p class="modal-about">About this Project ©2020</p>
        <div class="modal-bg">
          <div class="modal">
            <img src="./assets/me2.jpg" class="myPhoto" alt="photo">
            <h3>David Drobnak</h3>
            <p>Hey! I am David and I am the creator of this project.
              I made this project mostly just to practice my coding skills and learn how to use Vue.
              This SPA was made with Vue.JS, HTML5, CSS3 and some vanilla Javascript.
            </p>
            <a href="https://github.com/DavidDrob/"><img class="contact" src="./assets/github.svg" alt="github icon"></a>
            <span class="modal-close">X</span>
          </div>
        </div>
      </div>
      <div class="exercise-select">
        <input placeholder="#" maxlength='1' type="text" class="numberSearch" v-on:keyup.enter="createGivenId()">
        <button class='searchIcon' @click="createGivenId()">
          <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-search" fill="#33384A" xmlns="http://www.w3.org/2000/svg">
  <path fill-rule="evenodd" d="M10.442 10.442a1 1 0 0 1 1.415 0l3.85 3.85a1 1 0 0 1-1.414 1.415l-3.85-3.85a1 1 0 0 1 0-1.415z"/>
  <path fill-rule="evenodd" d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"/>
</svg>
        </button>
        <button class="next" @click="createRandomId()">Nächste Beispiel</button>
      </div>
    </footer>
  </div>
</template>

<script>
import task from './components/task.vue';
import answers from './components/answers.vue';
import canvasComp from './components/canvas.vue'


export default {
  name: 'App',
  data: function(){
    return{
      IdExercise: 0,
      done: []
    }
  },
  components: {
    task,
    answers,
    canvasComp
  },
  mounted(){
    let randid = Math.floor(Math.random()*10)
    this.IdExercise = randid

    var modalSelect = document.querySelector('.modal-about');
    var modalBg = document.querySelector('.modal-bg');
    var modalClose = document.querySelector('.modal-close');

    modalSelect.addEventListener('click',function(){
      modalBg.classList.add('bg-active');
    })
    modalClose.addEventListener('click',function(){
      modalBg.classList.remove('bg-active');
    })
  },
  methods:{
    createRandomId(){
      
      this.randid = Math.floor(Math.random()*10)
      console.log(this.done)
      while(this.randid in this.done){
        this.createRandomId()
      }
      this.IdExercise = this.randid
    },
    createGivenId(){
      this.randid = document.querySelector('.numberSearch').value*1
      this.IdExercise = this.randid
    }
  }
}
</script>

<style>
@keyframes modalAnimation {
  from {
    top: 200px;
    opacity: 0;
  }
  to {
    top: 0px;
  opacity: 1;
  }
}

@font-face {
  font-family: 'roboto-thin';
  src: url('./assets/fonts/roboto-thin.ttf');
}

@font-face {
  font-family: 'roboto-light';
  src: url('./assets/fonts/roboto-light.ttf');
}

body{
  background: url('./assets/grid.png');
  font-family: 'roboto-light';
}

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.modal-about:hover{
  padding-bottom: 3px;
  border-bottom: 2px #33384A solid;
  cursor: pointer;
}

.modal-bg{
  position: fixed;
  width: 100%;
  height: 100vh;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  visibility: hidden;
  opacity: 0;
}

.bg-active{
  visibility: visible;
  opacity: 1;
}

.modal{
  position: relative;
  background-color: #33384A;
  color: white;
  width: 35%;
  height: 45%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  animation: modalAnimation 0.8s ease-in;
}

.modal p{
  width: 80%;
  text-align: center;
}

.contact{
  margin-top: 20px;
}

.modal-close{
  position: absolute;
  top: 10px;
  right: 10px;
  font-weight: bold;
  cursor: pointer;
}

h3{
  font-size: 32px;
  padding-top: 180px;
  padding-bottom: 20px;
  font-family: 'roboto-thin';
}

.modal .myPhoto{
  max-height: 200px;
  border-radius: 50%;
  margin-bottom: 50px;
  position: absolute;
  top: 20px;
}

.about{
  z-index: 4;
}

.exercise-select{
  z-index: 5;
}

.task-component{
  margin: 30px 0px 0px 20px;
  z-index: 3;
}
.answers-component{
  margin-left: 20px;
  z-index: 2;
}
.canvas-component{
  position: absolute;
  z-index: 1;
}

footer{
  padding-top: 700px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 1780px;
}

.exercise-select, .about{
  margin-right: 40px;
}
.next{
  margin-left: 40px;
}

.exercise-select{
  display: flex;
  align-items: center;
}

input{
  outline: 0;
  border-width: 0 0 2px;
  height: 40px;
  width: 60px;
}

input:focus{
  border-color: #33384A;
}

::-webkit-input-placeholder{
  text-align: center;
}

:-moz-placeholder{
  text-align: center;
}

.numberSearch{
  text-align: center;
}

.searchIcon{
  padding: 0;
  outline: none;
  background: none;
  color: white;
  cursor: pointer;
  margin-left: 20px;
}

.searchIcon:hover{
    transform: none;
  transition: none;
  filter: none;
}

button:hover{
  transform: translateY(-15px);
  -webkit-transform: translateY(-15px);
  -ms-transform: translateY(-15px);
  transition: .3s ease;
  filter: drop-shadow(0 10px 4px #484b55);
}

</style>
