<template>

    <div id="sidebar">
      <Slider :title="partsNumSliderName" 
      :min="1" max="500" :step="1" :val="partsNumSliderValue" 
      @update="updateValue"></Slider>
      
      <Slider :title="rndSeedSliderName" 
      :min="1" max="1000" :step="1" :val="rndSeedSliderValue" 
      @update="updateValue"></Slider>

    </div>
  
    <div id="viewer">
      <GeometryView :data="inputs" :path="path"></GeometryView>
    </div>

</template>
  
<script setup>
  import { ref, onBeforeMount, computed } from "vue"
  import GeometryView from "../components/TestGeometryView.vue"
  import Slider from '../components/Slider.vue'

  
  //define path to grasshopper script
  import def from "../assets/wasp.gh"
  const path = def
  
  //define input names and values
  const partsNumSliderName = ref("parts_num")
  const partsNumSliderValue = ref(50)

  const rndSeedSliderName = ref("rnd_seed")
  const rndSeedSliderValue = ref(0)


  
  //define inputs
  let inputs = ref({
    [partsNumSliderName.value]: partsNumSliderValue.value ,
    [rndSeedSliderName.value]: rndSeedSliderValue.value ,
  });
  
  function updateValue(newValue, parameterName) {
    // Iterate over the inputs array
    for (const [key, value] of Object.entries(inputs.value)) {
      if (key == parameterName){
          inputs.value[key] = newValue
          console.log(parameterName + ':' + newValue)
      }
    }
  }
  
  </script>
  
  <style scoped>
  
  #sidebar {
    width: 310px;
    padding: 10px;
    flex-shrink: 0; 
  }
  
  #viewer { 
    width: 500px
  }
  
  </style>