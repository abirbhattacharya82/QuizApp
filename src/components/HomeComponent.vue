<template>
  <TitleComponent />
  <FunctionComponent />
  <InstructionComponent />
  <div class="StartArea">
    <button>Start</button>
  </div>
</template>

<script>
import TitleComponent from './TitleComponent.vue';
import FunctionComponent  from './FunctionComponent.vue';
import InstructionComponent from './InstructionComponent.vue';
export default{
  name:'HomeComponent',
  components:{
    TitleComponent,
    FunctionComponent,
    InstructionComponent
}
}
</script>