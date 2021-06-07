<template>
  <div
    class="region-background"
    :style="{ 'background-image': 'url(' + background_url + ')' }"
  >
   <SnowyCanvas v-if="weather==='snow'"/>
  </div>
</template>

<script>
import SnowyCanvas from "./SnowyCanvas";
export default {
  components: {
    SnowyCanvas,
  },
  props: {
    background_url: {
      type: String,
      required: true,
      default: "https://source.unsplash.com/1600x900/?safari",
    },
    weather:{
      type:String
    }
  },
  data(){
   return {testSwitch:"ABC"}
  },
 
    
  
};
</script>

<style>
.region-background {
  /* background: url() center/cover; */
  /* background: url("https://source.unsplash.com/1600x900/?london") center/cover; */
  background-position: bottom;
  height: 100%;
  min-height: 100vh;
  min-width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  z-index: -5;
}
</style>>

