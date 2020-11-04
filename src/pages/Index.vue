<template>
  <q-page>
    <!-- <example-component
      title="Example component"
      active
      :todos="todos"
      :meta="meta"
    ></example-component> -->
    <div class="row-1">
      <span class="text-h3 text-weight-bold">PODCASSO </span>  <span class="text-weight-bold text-overline">BY SENTIENT.IO</span>
    </div>
  
    <div  class="row items-center justify-center" style="height:60em;">
      <div class="col-3">
          <the-form :data=DATA></the-form>
      </div>
      <div class="col-3 offset-md-4">        
        <h3>
          Convert written texts into 
          <span style="font-weight:bold; font-size:55px;">PODCASTS</span> using AI powered by sentient io 
        </h3>
      </div>
    </div>





  </q-page>
</template>

<script lang="ts">
import { Todo, Meta } from 'components/models'
import VOICE_DATA from '../data/voice-data.js'


import TheForm from 'components/TheForm.vue'
import { defineComponent, ref } from '@vue/composition-api'



export default defineComponent({
  name: 'PageIndex',
  components: { TheForm },
  setup () {

    const DATA = VOICE_DATA


    return { DATA }
  }
})
</script>

<style scoped>
  .row-1 {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
  justify-content:center;
  height : 20vh;
}
</style>