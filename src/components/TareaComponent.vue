<template>
<div>
  <b-container>
    <b-row>
      <b-col lg="4" md="6"
        v-for="(tarea,index) in this.Tareas"
        v-bind:key="index"
      >
          <b-card-group deck>
            <b-card
              border-variant="solid dark"
              header-bg-variant="success"
              header-text-variant="white"
              :header="tarea.fecha_vencimiento"
              header-tag="header"
              footer="Card Footer"
              footer-tag="footer"
              :title="tarea.nombre"
            >
            <b-card-text>Header and footers using props.</b-card-text>
            <b-button href="#" variant="primary">Go somewhere</b-button>
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
    Tareas: Array
  },
  mounted () {
    this.Tareas.map(item => {
      console.log(item.nombre)
    })
  }
}

</script>
