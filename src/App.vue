<template>
  <div>
    <template v-if="currentHash != ''">
      <NavBar />
      <div v-if="currentHash === '#/users'">
        <TablaDeUsuarios :usuarios=usuarios :actualizarUsuarioSeleccionado=actualizarUsuarioSeleccionado
          :borrar=deleteUser />
      </div>
      <div v-else-if="currentHash === '#/agregar-usuario'">
        <FormularioUsuario :editar=editUser :agregar=addUser :usuarioSeleccionado=usuarioSeleccionado />
      </div>
      <FooterSection />
    </template>
    <template v-else>
      <LoginForm />
    </template>
  </div>
</template>

<script>

import FooterSection from './components/FooterSection.vue';
import NavBar from './components/NavBar.vue';
import TablaDeUsuarios from './components/TablaDeUsuarios.vue';
import FormularioUsuario from './components/FormularioUsuario.vue';
import LoginForm from "./components/login/LoginForm.vue";
import "./assets/styles.css"

const initialUserForm = {
  idSeleccionado: "",
  name: "",
  username: "",
  email: "",
  avatar: ""
}
export default {
  name: 'App',
  components: {
    NavBar,
    FooterSection,
    TablaDeUsuarios,
    FormularioUsuario,
    LoginForm
  },
  data() {
    return {
      usuarios: [],
      url: "https://fabrizio112.pythonanywhere.com/users",
      error: false,
      loading: true,
      usuarioSeleccionado: initialUserForm,
      currentHash: window.location.hash
    }
  },
  methods: {
    getUsers(url) {
      fetch(url)
        .then(res => res.json())
        .then(data => {
          this.usuarios = data
        })
        .catch(error => {
          this.error = true
          console.error(error)
        })

    },
    addUser(usuario) {
      let options = {
        body: JSON.stringify(usuario),
        method: 'POST',
        headers: { 'Content-Type': 'application/json' }
      }
      fetch(this.url, options)
        .then(res => res.json())
        .then(data => {
          alert("Usuario Creado")
          window.location.href = "#/users"
        })
        .catch(error => {
          console.error(error)
        })
    },
    deleteUser(id) {
      let options = {
        method: 'DELETE',
        headers: { 'Content-Type': 'application/json' },
        redirect: 'follow'
      }
      fetch(this.url + `/${id}`, options)
        .then(res => res.json())
        .then(data => {
          alert("Usuario Eliminado")
          location.reload()
        })
        .catch(error => {
          console.error(error)
        })
    },
    editUser(usuario, id) {
      let options = {
        body: JSON.stringify(usuario),
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        redirect: 'follow'
      }
      fetch(this.url + `/${id}`, options)
        .then(res => res.json())
        .then(data => {
          alert("Usuario Editado con Exito")
          window.location.href = "#/users"
        })
        .catch(error => {
          console.error(error)
        })
    },
    changeIdSeleccionado(id) {
      this.usuarioSeleccionado.idSeleccionado = id
    }, actualizarUsuarioSeleccionado(usuario) {
      this.usuarioSeleccionado = usuario
    },
    actualizarHash() {
      this.currentHash = window.location.hash
    }
  },
  created() {
    this.getUsers(this.url)
    window.addEventListener("hashchange", this.actualizarHash)
  }
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
</style>
