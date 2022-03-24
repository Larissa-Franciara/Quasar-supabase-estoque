<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title class="text-center">

          <q-avatar size="50px">
            <img src="https://images.vexels.com/media/users/3/130943/isolated/lists/6ce6689b20ca2489fed316da0c187450-etiqueta-de-diamante-moderno.png">
          </q-avatar>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, onMounted} from 'vue'
import useApi from "src/composables/UseApi";


export default defineComponent({
  name: 'LoginLayout',


  setup () {

    const {getBrand} = useApi()

    onMounted(() => {
      getBrand()
    })

    return {

      }
    }
})
</script>
