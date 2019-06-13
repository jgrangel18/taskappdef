<template>
  <div>
    <b-modal
      v-model="modalShow"
      id="modal-prevent-closing"
      ref="modal"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <b-container>
        <b-card-group deck>
          <b-card
            border-variant="solid dark"
            header-bg-variant="primary"
            header-text-variant="white"
            header='Crear una nueva Tarea'
          >
          <b-list-group flush>

            <form ref="form" @submit.stop.prevent="handleSubmit">
                <b-form-group
                  :state="nameState"
                  label="fecha_vencimiento"
                  label-for="date-input"
                  invalid-feedback="Name is required"
                >
                  <b-form-input
                    id="fecha_vencimiento"
                    v-model="tarea.fecha_vencimiento"
                    :state="nameState"
                    type="date"
                    required
                  ></b-form-input>

                </b-form-group>
                <b-form-group
                  :state="nameState"
                  label="nombreTarea"
                  label-for="name-input"
                  invalid-feedback="Name can not be empty"
                >
                  <b-form-input
                    id="nombreTarea"
                    v-model="tarea.nombreTarea"
                    :state="nameState"
                    required
                  ></b-form-input>

                </b-form-group>
                <b-form-group
                  :state="nameState"
                  label="Frecuencia"
                  label-for="frecuencia-input"
                  invalid-feedback="Frecuency is required"
                >
                <b-form-select
                  v-model="tarea.frecuencia"
                  :options="tipo_tarea"
                  :state="nameState"
                >

                </b-form-select>

                </b-form-group>
                <b-form-group
                  :state="nameState"
                  label="Hora"
                  label-for="time-input"
                  invalid-feedback="Time is required"
                >
                  <b-form-input
                    id="tasktime"
                    v-model="tarea.hora"
                    type="time"
                    :state="nameState"
                    required
                  ></b-form-input>

                </b-form-group>
            </form>
          </b-list-group>
          </b-card>
        </b-card-group>
      </b-container>
    </b-modal>
  </div>
</template>
<script>
export default {
  props: {
     modalShow:Boolean
  },
    data () {
    return {
      tipo_tarea: [
        { value: null, text: 'Escoga Tarea' },
        { value: 'Diaria', text: 'Diaria' },
        { value: 'Semanal', text: 'Semanal' },
        { value: 'Mensual', text: 'Mensual' },
        { value: 'Trimestral', text: 'Trimestral' }
      ],
      selected: null,
      nameState: null,
      tarea: {
        id: 0,
        nombreTarea: '',
        frecuencia: '',
        fecha_vencimiento: '',
        status: 0,
        responsable_id: this.$route.params.id,
        hora: ''
      }

    }
  },
  methods: {
    checkFormValidity () {
      const valid = this.$refs.form.checkValidity()
      this.nameState = valid ? 'valid' : 'invalid'
      return valid
    },
    resetModal () {
      this.tarea.fecha_vencimiento = ''
      this.tarea.nombreTarea = ''
      this.tarea.frecuencia = ''
      this.tarea.status = ''
      this.tarea.hora = ''
      this.nameState = null
    },
    handleOk (bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault()
      // Trigger submit handler
      this.handleSubmit()
    },
    handleSubmit () {
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return
      }
      this.$nextTick(() => {
        this.$refs.modal.hide()
      })
    }

  }
}
</script>
