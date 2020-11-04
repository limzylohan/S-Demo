<template>
    <div class="q-pa-md row items-start q-gutter-md">
    <q-card class="my-card">
        <div class="col">
         <q-card-section
          v-morph:button:boxes:800="morphGroupModel">
            <div v-if="new_val===false" class="q-gutter-sm row items-start">
                <q-uploader
                    label="It's as simple as just uploading your script."
                    color="purple"
                    square
                    flat
                    bordered
                    accept=".txt"
                    style="max-width: 300px"
                    @added="attachedFile"
                />
            </div>
            <div v-else class="row items-center justify-center">
                <strong>Click Generate Podcast to start</strong>
                <q-uploader
                    color="white"
                    style="max-width: 300px"
                    @added="attachedFile"
                />
            </div>
            <div class="row items-center justify-center">
                <q-checkbox v-model="val" 
                />
                SSML
            </div>
                <br>

            <div class="row items-center justify-center">
               <strong>Choose Gender</strong>
            </div>     


            <div class="row items-center justify-center" style='background-color:red;'>
            <q-btn-toggle
                style="width:100%"
                v-model="gender"
                spread
                toggle-color="purple"
                color="white"
                text-color="black"
                push
                :options="[
                {label: 'male', value: 'male'},
                {label: 'female', value: 'female'}
                ]"
            />            
            </div>     

            <div class="row items-center justify-center">
                <br>
                 <strong>Choose Voice Model</strong> 
            </div>   

            <div class="row items-center justify-center">
                <q-select style="width:100%" 
                borderless v-model="audioWave" 
                :options="data"
                counter
                menu-self="bottom left"
                />            
            </div>   

            <div v-if="new_val" class="row items-center justify-center" >
                <q-btn color="purple" label="Generate Podcast"  style="width:100%"
                @click='nextMorph'
                />
            </div>  

      </q-card-section>

                    <div
                    v-morph:loader:boxes:600.tween="morphGroupModel"
                    >
                        <img src="../assets/spinner.svg">
                    </div>
        </div>
    </q-card>
                    <div
                    v-morph:newpage:boxes:600.tween="morphGroupModel"
                    >

                        Audio Ready
                        <audio controls>
                            <source src="horse.ogg" type="audio/ogg">
                        </audio>

                        <div class="row items-center justify-center" >
                            <q-btn color="purple" label="Start Again"  style="width:100%"
                            @click='nextMorph'
                            />
                        </div>  

                    </div>

    </div>
</template>

<script lang="ts">
import {
  defineComponent, PropType, computed, ref, toRef, watch
} from '@vue/composition-api'
import { morph } from 'quasar'
import { Data } from './models'



export default defineComponent({
  name: 'TheForm',
  props: {
    data : {
        type: (Array as unknown) as PropType<Data[]>,
        required : true
    }
  }, setup() {
      const audioWave = ref<String>("en-GB-Wavenet-F")
      const val = ref<boolean>(false)
      const gender = ref<String>("male")
      const fileName = ref<String>("")
      const isFileLoaded = ref<boolean>(false)
      const new_val = ref<boolean>(false)
      const morphGroupModel = ref<String>('button')

    
      const attachedFile = (files) => {
          isFileLoaded.value = true
          fileName.value = files[0].name
          new_val.value = true
      }

      function nextMorph() {
          console.log("running Next Morph")
          let value = morphGroupModel.value
          if (value == "button") {
              morphGroupModel.value = "loader"
          } else if (value =="loader") {
              morphGroupModel.value = "newpage"
          } else if (value =="newpage") {
              morphGroupModel.value = "button"
          }  
      }

      watch(morphGroupModel, (newVar,oldVar) => {
          console.log(oldVar)
          console.log(newVar)
          if (newVar == "loader") {
              console.log("running set time out")
              setTimeout(() => {
                  morphGroupModel.value = "newpage"
              }, 5000)
          }
      })
        


        

      return {audioWave, val, gender, fileName, attachedFile, isFileLoaded, new_val, nextMorph, morphGroupModel}
  }

})
</script>
