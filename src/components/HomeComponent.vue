<template>
  <TitleComponent />
  <!-- <FunctionComponent /> -->
  <InstructionComponent v-if="show"/>
  <div class="StartArea">
    <button @click="startQuiz()" id="startButton">Start</button>
  </div>
</template>

<script>
import TitleComponent from './TitleComponent.vue';
// import FunctionComponent  from './FunctionComponent.vue';
import InstructionComponent from './InstructionComponent.vue';
export default{
  data(){
    return{
      show:true
    }
  },
  name:'HomeComponent',
  components:{
    TitleComponent,
    // FunctionComponent,
    InstructionComponent
  },
  methods:{
    startQuiz(){
      this.show=false;
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