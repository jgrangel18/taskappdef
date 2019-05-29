<template>
<div>
  <TareaComponent
  v-bind:Tareas="Tareas"
  v-bind:TipoTarea="TipoTarea"
  >
  </TareaComponent>
</div>
</template>
<script>
import Tareas from '@/data/Tareas'
import TipoTarea from '@/data/TipoTarea'
import TareaComponent from '@/components/TareaComponent.vue'
export default {
  components: {
    TareaComponent
  },
  data () {
    return {
      Tareas: Tareas,
      TipoTarea: TipoTarea
    }
  }
}
</script>
