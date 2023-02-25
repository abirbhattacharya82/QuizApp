<template>
  <TitleComponent />
  <FunctionComponent v-if="showQuiz" />
  <InstructionComponent v-if="showIns"/>
  <div class="StartArea">
    <button @click="startQuiz()" id="startButton">Start</button>
  </div>
</template>

<script>
import TitleComponent from './TitleComponent.vue';
import FunctionComponent  from './FunctionComponent.vue';
import InstructionComponent from './InstructionComponent.vue';
export default{
  data(){
    return{
      showIns:true,
      showQuiz:false
    }
  },
  name:'HomeComponent',
  components:{
    TitleComponent,
    FunctionComponent,
    InstructionComponent
  },
  methods:{
    startQuiz(){
      this.showIns=false;
      this.showQuiz=true;
      document.getElementById('startButton').style.display="none";
    }
  }
}
</script>

<style>
.StartArea
{
  display: flex;
  justify-content: center;
}
.StartArea button
{
  background-color: rgb(64, 255, 47);
  color: white;
  border: none;
  padding: 1%;
  font-size: 150%;
}
.StartArea button:hover
{
  background-color: rgb(39, 150, 29);
}
</style>