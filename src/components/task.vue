<template>
    <div class="task-component">
        <div class="task-id">
            <h1>Beispiel: {{ filterById.id }}</h1>
        </div>
        <div class="task-formula">
            <h2>{{ filterById.formula }}</h2>
        </div>
        <div class="task-description">
            <h2>{{ filterById.description }}</h2>
            <img class="imageSize" v-if="filterById.id == 7 || filterById.id == 6" :src="getImgUrl(filterById.image)">
        </div>
    </div>
</template>

<script>
import exerciseJson from "../assets/bsp.json";

export default {
  name: 'Task',
  props: ['exId'],
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
    getImgUrl(path) {
      var images = require.context('../assets/img/')
      return images('./' + path + ".png")
  }
  }
}
</script>

<style>
@font-face {
  font-family: 'roboto-thin';
  src: url('../assets/fonts/roboto-thin.ttf');
}

.task-id{
  margin-bottom: 15px;
  font-family: 'roboto-thin';
  margin-left: -3px;
  letter-spacing: 3px;
}

.imageSize{
  position: absolute;
  margin-top: 20px;
  width: 800px;
  height: auto;
}

</style>