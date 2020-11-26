<template>
    <div class="answers-component">
        <ul>
            <li v-for="answer in filterById.answers"
            :key="answer.answerInput">
            <button class="aniButton" @click="checkAnswer(answer)">{{answer.answerInput}}</button></li>
        </ul>
    </div>
</template>

<script>
import exerciseJson from "../assets/bsp.json";

export default {
  name: 'Answers',
  props: ['exId', 'doneList'],
  data: function(){
    return{
    exercises: exerciseJson.exercises,
    }
  },
  computed:{
    filterById(){
      return this.exercises.find(exercises => exercises.id === this.exId)
    }
  },
  methods:{
  checkAnswer (answer){
      if (answer.correct == true){
        event.target.classList.add('correct');
        event.target.classList.remove('aniButton');
        
        this.doneList.push(this.exId);
      }
      else{
        event.target.classList.add('notCorrect');
        event.target.classList.remove('aniButton');
      }
    },
  }
}
</script>

<style>
@keyframes notCorrectAnimation {
  0%{
    transform: translateX(0px);
  }
  25%{
    transform: translateX(-12px);
  }
  50%{
    transform: translateX(12px);
  }
  100%{
    transform: translateX(0);
  }
}

@keyframes correctAnimation{
  0%{
    transform: scale(1);
  }
  25%{
    transform: scale(1.2);
  }
  75%{
    transform: scale(1.2);
  }
  90%{
    transform: scale(1.1);
  }
  100%{
    transform: scale(1);
  }
}

.correct{
  animation: correctAnimation 0.8s linear;
  background: #01C851;
}

.notCorrect{
  animation: notCorrectAnimation 200ms linear;
  background: #FF3548;
}


ul{
  display: flex;
  list-style: none;
}

li{
  margin-right: 40px;
}
li:last-child{
  padding: 0;
}

button{
  font-size: 24px;
  padding: 25px 30px 25px 30px;
  border: none;
  outline: none;
  background: #33384A;
  color: white;
  cursor: pointer;
}


</style>