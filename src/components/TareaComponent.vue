<template>
<div>
  <b-container>
    <h1> {{ $route.params.id }} </h1>
    <b-row>
      <b-col lg="3" md="3"
        v-for="(tarea,index) in getArray"
        v-bind:key="index"
      >
          <b-card-group deck>
            <b-card
              border-variant="solid dark"
              header-bg-variant="primary"
              header-text-variant="white"
              :title="tarea.nombreTarea"
              :header="tarea.fecha_vencimiento"
            >
            <!-- :footer="test" -->
            <!-- :header="getfrequency(tarea.tipo_tarea)" -->
            <b-list-group flush>
              <b-list-group-item><b>Frecuencia:</b> {{tarea.frecuencia}}</b-list-group-item>
              <b-list-group-item><b>Color:</b> {{tarea.color}}</b-list-group-item>
              <b-list-group-item><b>Status:</b> {{tarea.status}}</b-list-group-item>
            </b-list-group>
            <b-button href="#" variant="primary">Edit</b-button>
            </b-card>
          </b-card-group>
          <br>
        </b-col>
  </b-row>
  </b-container>
</div>
</template>
<script>
export default {
  props: {
    Tareas: Array,
    TipoTarea: Array,
    Responsables: Array
  },
  data () {
    return {
      mixTareas:
      [
        {
          'nombreTarea': '',
          'frecuencia': '',
          'color': '',
          'fecha_vencimiento': '',
          'status': '',
          'responsablename': '',
          'responsable_id': '',
          'name': '',
          'lastname': '',
          'dob': '',
          'age': '',
          'username': '',
          'email': ''

        }
      ]
    }
  },
  methods: {
    getfrequency (id_tipo_tarea) {
      this.TipoTarea.map(tarea => {
        if (id_tipo_tarea === tarea.id) {
          console.log('SI LA ENCONTRE Y ES' + tarea.nombre)
          return tarea.nombre
        }
      })
    },
    imprimir () {
      this.mixTareas.map(tarea => {
        console.log(tarea.nombreTarea)
        console.log(tarea.frecuencia)
        console.log(tarea.color)
        console.log(tarea.fecha_vencimiento)
        console.log(tarea.status)
      })
    }
  },
  computed: {
    getArray () {
      const arr = this.mixTareas.filter((item, index) => {
        return index > 0 // will return the array from the second value
      })
      return arr
    }
  },
  mounted () {
    for (let iterator of this.Tareas) {
      console.log(iterator.nombre)
      for (let item of this.TipoTarea) {
        if (iterator.tipo_tarea === item.id) {
          console.log(item.nombre)
          this.mixTareas.push({
            'nombreTarea': iterator.nombre,
            'frecuencia': item.nombre,
            'color': item.color,
            'fecha_vencimiento': iterator.fecha_vencimiento,
            'status': iterator.status
          })
        }
      }
      for (let resp of this.Responsables) {
        if (iterator.responsable_id === resp.id) {
          console.log('EXISTO' + resp.name);
        }
      }
    }
    this.imprimir()
  }
}

</script>
