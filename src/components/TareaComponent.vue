<template>
<div>
  <b-container>
    <br>
    <b-row>
      <b-col lg="3" md="3"
        v-for="(tarea,index) in this.getArray"
        v-bind:key="index"
      >
          <b-card-group deck>
            <b-card
              border-variant="solid dark"
              header-bg-variant="primary"
              header-text-variant="white"
              :title="tarea.nombreTarea"
              :header="'FECHA:'+tarea.fecha_vencimiento"
            >
            <!-- :footer="test" -->
            <!-- :header="getfrequency(tarea.tipo_tarea)" -->
            <b-list-group flush>
              <b-list-group-item><b>Frecuencia:</b> {{tarea.frecuencia}}</b-list-group-item>
              <b-list-group-item><b>Time:</b>{{tarea.hora}} </b-list-group-item>
              <b-list-group-item><b>Status:</b> {{tarea.status}}</b-list-group-item>
            </b-list-group>
            <br>
            <b-button v-on:click="updatetask(tarea.id)" variant="primary" class="btn-space">Editar</b-button>
            <b-button v-on:click="removetask(tarea.id)" class="btn-space" variant="primary">Eliminar</b-button>
            </b-card>
          </b-card-group>
          <br>
        </b-col>
  </b-row>
  <NewTask
    v-bind:addarray="addarray"
    v-bind:tamanioarray="tamanioarray"
  >
  </NewTask>
  <UpdateTask
  v-bind:modalShow="modalShow"
  >  
  </UpdateTask>
  </b-container>

</div>
</template>
<script>
import NewTask from '@/components/NewTask.vue'
import UpdateTask from '@/components/UpdateTask.vue'
export default {
  components: {
    NewTask,
    UpdateTask
  },
  props: {
    Tareas: Array,
    TipoTarea: Array,
    Responsables: Array
  },
  data () {
    return {
      mixTareas: [],
      tamanioarray: 0,
      modalShow:false
    }
  },
  methods: {
    getfrequency (id_tipo_tarea) {
      this.TipoTarea.map(tarea => {
        if (id_tipo_tarea === tarea.id) {
          return tarea.nombre
        }
      })
    },
    imprimir () {
      this.mixTareas.map(tarea => {
        console.log(tarea.id);
        console.log(tarea.nombreTarea)
        console.log(tarea.name)
        console.log(tarea.color)
        console.log(tarea.fecha_vencimiento)
        console.log(tarea.status)
      })
    },
    addarray (tareaobject) {
      this.mixTareas.push({
        id: tareaobject.id,
        nombreTarea: tareaobject.nombreTarea,
        frecuencia: tareaobject.frecuencia,
        fecha_vencimiento: tareaobject.fecha_vencimiento,
        status: tareaobject.status,
        responsable_id: tareaobject.responsable_id,
        hora: tareaobject.hora
      });
      this.tamanioarray = this.mixTareas.length;
      // console.log('ID' + tareaobject.id);
      // console.log('NOMBRE TAREA' + tareaobject.nombreTarea);
      // console.log('FRECUENCIA' + tareaobject.frecuencia);
      // console.log('Fecha Vencimiento' + tareaobject.fecha_vencimiento);
      // console.log('Status' + tareaobject.status);
      // console.log('Responsable ID' + tareaobject.responsable_id);
      // console.log('HORA' + tareaobject.hora);
    },
    removetask (index) {
      console.log(index);
      this.mixTareas = this.mixTareas.filter(tarea => {
        console.log(tarea.id);
        return tarea.id !== index
      })
    },
    updatetask () {
      this.modalShow = !this.modalShow;
    }
  },
  
  computed: {
    getArray () {
      const arr = this.mixTareas.filter((tarea, index) => {
        return tarea.responsable_id == this.$route.params.id // will return the array from the second value
      })
      return arr
    }
  },
  mounted () {
    let displaytarea = {};
    displaytarea = {
      id: '',
      nombreTarea: '',
      frecuencia: '',
      color: '',
      fecha_vencimiento: '',
      status: '',
      responsable_id: '',
      hora: '',
      name: '',
      lastname: '',
      dob: '',
      age: '',
      username: '',
      email: ''
    }
    for (let iterator of this.Tareas) {
      for (let item of this.TipoTarea) {
        if (iterator.tipo_tarea === item.id) {
          displaytarea.frecuencia = item.nombre;
          displaytarea.color = item.color;
          displaytarea.fecha_vencimiento = iterator.fecha_vencimiento;
          displaytarea.nombreTarea = iterator.nombre;
          displaytarea.status = iterator.status;
        }
      }
      for (let resp of this.Responsables) {
        if (iterator.responsable_id === resp.id) {
          displaytarea.name = resp.name
          displaytarea.lastname = resp.lastname;
          displaytarea.dob = resp.dob;
          displaytarea.age = resp.age;
          displaytarea.username = resp.username;
          displaytarea.email = resp.email;
          displaytarea.responsable_id = resp.id;
        }
      }
      displaytarea.id = iterator.id
      displaytarea.hora = iterator.hora
      this.addarray(displaytarea);
    }
    // this.imprimir();
    // console.log(this.mixTareas.length);
    // console.log(this.tamanioarray);
  }
}

</script>
<style lang="scss">
 .btn-space {
    margin-right: 5px;
}
</style>
