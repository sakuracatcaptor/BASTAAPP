<template>
  
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Juega Basta</ion-title>
        

      </ion-toolbar>
      <p v-if="state.isOver"> Tiempo terminado </p> 

    </ion-header>

    <ion-content :fullscreen="true">
       <ion-text color="danger">
          <h1>{{ formattedTime }}</h1>
        </ion-text>
      <!-- <p>Para jugar basta da clic en iniciar, empezará a correr el tiempo. Da clic en la letra que jugaste para reiniciar el tiempo. Si se termina el tiempo o las letras, da clic en el botón iniciar para reiniciar la partida.</p>     -->
      <ion-button @click="startTimer" :disabled="isRunning" color="success" expand="block">Iniciar</ion-button>
      <ion-list>
        <ion-label v-for="tecla in teclas" :key="tecla.id">
          <ion-button @click="clicLetra(tecla), resetTimer()" :disabled="tecla.disabled" size="large" shape="round">{{ tecla.label }}</ion-button>
        </ion-label>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonLabel, IonList} from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';



</script>

//Script para botones
    <script lang="ts">
      import { IonButton } from '@ionic/vue';
      import { defineComponent } from 'vue';

      export default defineComponent({
        components: { IonButton },
      });

//Script de basta
import { reactive, computed, ref, onBeforeUnmount } from 'vue'

// Estado inicial
const state = reactive({
  seconds: 10,
  isOver: false
})

const isRunning = ref(false)
let interval = null

// Formatear el tiempo
const formattedTime = computed(() => {
  const minutes = Math.floor(state.seconds / 60).toString().padStart(2, '0')
  const secs = (state.seconds % 60).toString().padStart(2, '0')
  return `${minutes}:${secs}`
})

// Función para iniciar el timer
function startTimer() {
  if (state.seconds == 0) {
    state.seconds = 10;
  }

  if (isRunning.value) return

  isRunning.value = true

  interval = setInterval(() => {
    if (state.seconds > 0) {
      state.seconds--
    } else {
      clearInterval(interval)
      isRunning.value = false
      state.isOver = true
    }
  }, 1000)
  resetKeyWord()
}

function resetTimer () {
    state.seconds = 10;

    if (isRunning.value) return

  isRunning.value = true

  interval = setInterval(() => {
    if (state.seconds > 0) {
      state.seconds--
    } else {
      clearInterval(interval)
      isRunning.value = false
      state.isOver = true
    }
  }, 1000)
}

// Limpiar el interval si el componente se desmonta
onBeforeUnmount(() => {
  clearInterval(interval)
})

// Teclado script

const teclas = ref([
    {id: 1, label: "A", color: "green", disabled: false},
    {id: 2, label: "B", color: "green", disabled: false},
    {id: 3, label: "C", color: "green", disabled: false},
    {id: 4, label: "D", color: "green", disabled: false},
    {id: 5, label: "E", color: "green", disabled: false},
    {id: 6, label: "F", color: "green", disabled: false},
    {id: 7, label: "G", color: "green", disabled: false},
    {id: 8, label: "H", color: "green", disabled: false},
    {id: 9, label: "I", color: "green", disabled: false},
    {id: 10, label: "J", color: "green", disabled: false},
    {id: 11, label: "K", color: "green", disabled: false},
    {id: 12, label: "L", color: "green", disabled: false},
    {id: 13, label: "M", color: "green", disabled: false},
    {id: 14, label: "N", color: "green", disabled: false},
    {id: 15, label: "O", color: "green", disabled: false},
    {id: 16, label: "P", color: "green", disabled: false},
    {id: 17, label: "R", color: "green", disabled: false},
    {id: 18, label: "S", color: "green", disabled: false},
    {id: 19, label: "T", color: "green", disabled: false},
    {id: 20, label: "U", color: "green", disabled: false},
    {id: 21, label: "V", color: "green", disabled: false},

])

function clicLetra(tecla){
    tecla.disabled=true
}
function resetKeyWord(){
     teclas.value.forEach((e) => e.disabled=false);
     state.isOver= false
    //  ;

        // console.log(e)
}
function PartidaEnd(){
     teclas.value.forEach((e) => e.disabled=false);
     state.isOver= false
    //  ;

        // console.log(e)
}

    </script>

    <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  font-size: 5em;
}
ion-label ion-list{
    display: inline-block;
    list-style-type: none;
    padding: 4px;

}
ion-label ion-list button {
    padding: 8px;
    background-color: blueviolet;
    border-color: aliceblue;
}
</style>