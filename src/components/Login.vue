<template>
  <div>
    <b-container>
       <b-jumbotron header="Bootstrap Taskapp">
         <br>
        <form @submit="validate()" >
          <h1 class="display-4 text-center"></h1>
          <div class="form-group row col-sm-8 offset-sm-2 text-center">
            <label for="email" class="col-sm-4 col-form-label">Email address:</label>
            <div class="col-sm-6">
              <input type="email" v-model="user.email"  class="form-control" id="email">
            </div>
          </div>
          <div class="form-group row col-sm-8 offset-sm-2 text-center">
            <label for="pwd" class="col-sm-4 col-form-label">Password:</label>
            <div class="col-sm-6">
              <input v-model="user.password" type="password" class="form-control" id="pwd">
            </div>
          </div>
          <br>
          <div class="form-group row col-sm-6 offset-sm-5 text-center">
            <button id="submit" v-on:click.prevent="validate()" type="submit" class="btn btn-primary col-sm-3 col-form-label" >Submit</button>
            <div class="col-sm-2 text-center">
              <button id="reg" value="submit" type="submit"  class="btn btn-primary col-form-label d-none">
                Register
              </button>
            </div>
          </div>
          <b-button id="loading" variant="primary" disabled class="btn-lg d-none">
            <b-spinner small type="grow"></b-spinner>
            Loading...
          </b-button>
            <br>
            <br>
          <div v-if="errproblem===true" >

            <div v-for="error in errors" v-bind:key="error">
              <li>
                  {{error}}
              </li>
            </div>
          </div>
        </form>
      </b-jumbotron>
    </b-container>
  </div>
</template>
<script>
import Responsables from '@/data/Responsables'

export default {

  props: ['username', 'password'],
  data () {
    return {
      user: {
        email: '',
        password: ''
      },
      responsables: Responsables,
      errors: [],
      errproblem: false,
      responsable: Object
    }
  },
  watch: {
    username: function () {
      this.user.email = this.username
    }
  },
  methods: {
    imprimir: function () {
      console.log(' email ' + this.user.email)
      console.log('usuario' + this.user.password)
    },
    element: function (parametro) {
      let elem = document.getElementById(parametro)
      return elem
    },

    validate: function () {
      this.errproblem = false
      this.errors = []
      let pwderr = this.element('pwd')
      let emailerr = this.element('email')
      if (this.user.email === '') {
        this.errors.push('El campo del correo no puede estar vacio')

        console.log(emailerr)
        console.log('EL CORREO NO PUEDE SER VACIO')
        this.errproblem = true
        document.getElementById('email').style.border = '1px solid red'
      } else if (this.user.password === '') {
        console.log(pwderr)
        this.errors.push('El campo de la contrasenia no puede ser vacio')
        console.log('el campo de la contrasenia no puede ser vacio')
        this.errproblem = true
        document.getElementById('pwd').style.border = '1px solid red'
      } else {
        this.validate_password()
      }
    },

    validate_password: function () {
      let find_responsable = []
      let find_password = []
      find_responsable = this.responsables.find(responsable => responsable.email === this.user.email || responsable.password === this.user.password)
      find_password = this.responsables.find(responsable => responsable.email === this.user.email && responsable.password === this.user.password)
      if (find_responsable === undefined) {
        this.errors.push('Su usuario no existe porfavor registrese')
        console.log('Su usuario no existe porfavor registrese')
        this.errproblem = true
        document.getElementById('reg').classList.remove('d-none')
      } else if (find_password === undefined) {
        this.errors.push('Brutalio ha escrito mal su contrasenia o usuario')
        console.log('Brutalio ha escrito mal su contrasenia o usuario')
        this.errproblem = true
      } else {
        document.getElementById('submit').classList.add('d-none')
        document.getElementById('loading').classList.remove('d-none')
        this.responsable = find_responsable
        setTimeout(() => {
          this.$router.push('/mytasks' + '/' + find_responsable.id)
          console.log(find_responsable);
        }, 5000)
      }
      console.log('ENCONTRE AL RESPONSABLES' + find_responsable)
      console.log('ENCONTRE LA PASSS' + find_password)
    },
    datauser: function () {
      // DECLARING MULTIPLE PROMISES AND FECTHING DATA!
      const responsablesPromise = fetch('./dataset/responsables.json')
      Promise
      // WAITING FOR ALL TO COMPLETE
        .all([responsablesPromise])
        .then(responses => {
          // CONVERTING AL PROMISES INTO JSON
          return Promise.all(responses.map(resp => resp.json()))
        })
      // FORMAT THE ANSWER TO GET MULTIPLE ARRAYS
        .then(respon => {
          console.log(respon)
          const [responsables] = respon.map(res => res)
          this.responsables = responsables
        })
        .catch((err) => {
          console.log(err)
        })
    }
  },
  mounted () {
    console.log('Cargando Info del los users');
  }

}
</script>
