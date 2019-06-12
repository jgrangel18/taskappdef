<template>
<div>
  <NavBar>
  </NavBar>
  <TareaComponent
  v-bind:Tareas="Tareas"
  v-bind:TipoTarea="TipoTarea"
  v-bind:Responsables="Responsables"
  >
  </TareaComponent>
</div>
</template>
<script>
import Tareas from '@/data/Tareas'
import TipoTarea from '@/data/TipoTarea'
import Responsables from '@/data/Responsables'
import TareaComponent from '@/components/TareaComponent.vue'
import NavBar from '@/components/NavBar.vue'

export default {
  components: {
    TareaComponent,
    NavBar
  },
  data () {
    return {
      Tareas: Tareas,
      TipoTarea: TipoTarea,
      Responsables: Responsables
    }
  }
}
</script>
