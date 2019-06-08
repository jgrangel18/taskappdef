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
              :header="tarea.fecha_vencimiento"
            >
            <!-- :footer="test" -->
            <!-- :header="getfrequency(tarea.tipo_tarea)" -->
            <b-list-group flush>
              <b-list-group-item><b>Frecuencia:</b> {{tarea.frecuencia}}</b-list-group-item>
              <b-list-group-item><b>Color:</b> {{tarea.color}}</b-list-group-item>
              <b-list-group-item><b>Responsable name:</b> {{tarea.name}} {{tarea.lastname}}</b-list-group-item>
              <b-list-group-item><b>dob:</b> {{tarea.dob}}</b-list-group-item>
            </b-list-group>
            <br>
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
      mixTareas: []
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
        color: tareaobject.color,
        frecuencia: tareaobject.frecuencia,
        fecha_vencimiento: tareaobject.fecha_vencimiento,
        status: tareaobject.status,
        responsable_id: tareaobject.responsable_id,
        name: tareaobject.name,
        lastname: tareaobject.lastname,
        dob: tareaobject.dob,
        age: tareaobject.age,
        username: tareaobject.username,
        email: tareaobject.email

      });
      // console.log(tareaobject.nombreTarea);
      // console.log(tareaobject.frecuencia);
      // console.log(tareaobject.color);
      // console.log(tareaobject.fecha_vencimiento);
      // console.log(tareaobject.status);
      // console.log(tareaobject.responsable_id);
      // console.log(tareaobject.name);
      // console.log(tareaobject.lastname);
      // console.log(tareaobject.dob);
      // console.log(tareaobject.age);
      // console.log(tareaobject.username);
      // console.log(tareaobject.email);
    }
  },
  computed: {
    getArray () {
      const arr = this.mixTareas.filter((tarea, index) => {
        console.log('responsable' + tarea.responsable_id);
        console.log('ruta parametro' + this.$route.params.id);
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
      this.addarray(displaytarea);
    }
    this.imprimir();
  }
}

</script>
