<template>

    <div id="sidebar">
      <Slider :title="heightSliderName" 
      :min="1" max="20" :step="1" :val="heightSliderValue" 
      @update="updateValue"></Slider>

      <Slider 
      :title="widthSliderName" 
      :min="1" max="20" :step="1" :val="widthSliderValue" @update="updateValue"></Slider>
      
      <Slider :title="depthSliderName" 
      :min="0" max="20" :step="1" :val="depthSliderValue" @update="updateValue"></Slider>

      <Slider :title="hieghtSliderName" 
      :min="0" max="20" :step="1" :val="heightSliderValue" @update="updateValue"></Slider>
      
    </div>
  
    <div id="viewer">
      <GeometryView :data="inputs" :path="path"></GeometryView>
    </div>

</template>
  
<script setup>
  import { ref, onBeforeMount, computed } from "vue"
  import GeometryView from "../components/TestGeometryView.vue"
  import Slider from '../components/Slider.vue'
  import Dropdown from "../components/Dropdown.vue"
  
  //define path to grasshopper script
  import def from "../assets/box.gh"
  const path = def
  
  //define input names and values
  const widthSliderName = ref("depth")
  const widthSliderValue = ref(10)
  
  const depthSliderName = ref("width")
  const depthSliderValue = ref(10)
  
  const hieghtSliderName = ref("height")
  const heightSliderValue = ref(10)


  
  //define inputs
  let inputs = ref({
    [widthSliderName.value]: widthSliderValue.value ,
    [depthSliderName.value] : depthSliderValue.value ,
    [hieghtSliderName.value] : heightSliderValue.value,
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