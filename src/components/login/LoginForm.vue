<template>
    <main id="main-login" class="w-100 d-flex justify-content-center align-items-center">
        <div class="bg-light" id="login-container">
            <section class="d-flex justify-content-center align-items-center gap-2 mb-4" id="section-buttons">
                <button class="btn btn-primary w-100 py-2" @click="handleChangeBoton">Iniciar Sesion</button>
                <button class="btn btn-dark w-100 py-2" @click="handleChangeBoton">Registrarse</button>
            </section>
            <div v-if="botonClickeado === 'Iniciar Sesion'">
                <IniciarSesion :login=loginUser />
            </div>
            <div v-else>
                <Registrarse :registrar=signUpUser />
            </div>

        </div>
    </main>
</template>

<script>
import Registrarse from './Registrarse.vue';
import IniciarSesion from './IniciarSesion.vue'
export default {
    name: "LoginForm",
    data() {
        return {
            botonClickeado: "Iniciar Sesion",
            urlSignUp: "https://fabrizio112.pythonanywhere.com/signup",
            urlLogin: "https://fabrizio112.pythonanywhere.com/login",
        }
    },
    components: {
        Registrarse,
        IniciarSesion
    },
    methods: {
        handleChangeBoton(e) {
            this.botonClickeado = e.target.innerText
        },
        signUpUser(user) {
            let options = {
                body: JSON.stringify(user),
                method: 'POST',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(this.urlSignUp, options)
                .then(response => {
                    if (response.status === 401) {
                        alert("Error Nombre de Usuario o Correo Existente")
                    } else if (response.status === 200) {
                        alert("Inicio de Sesion Exitoso")
                    }
                })

                .catch(error => {
                    console.error(error)
                })
        },
        loginUser(user) {
            let options = {
                body: JSON.stringify(user),
                method: 'POST',
                headers: { 'Content-Type': 'application/json' }
            }
            fetch(this.urlLogin, options)
                .then(response => {
                    if (response.status === 401) {
                        alert("Error Unathorized")
                    } else if (response.status === 200) {
                        alert("Inicio de Sesion Exitoso")
                    }
                })

                .catch(error => {
                    console.log(error)
                })
        }
    }
}

</script>

<style>
#main-login {
    min-height: 80vh;
}

#login-container {
    width: 400px;
    height: 500px;
    border-radius: 15px;
    color: black;
    padding: 2rem;
}

#section-buttons {
    height: 20%;
}
</style>
