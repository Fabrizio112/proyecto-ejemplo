<template>
    <div id="form-register">
        <h1 class="m-3 fs-3 ">Registrarse</h1>
        <form action="" class="gap-4 d-flex flex-column" @submit="handleRegister">
            <div class="row">
                <div class="col">
                    <input type="text" placeholder="Nombre" name="name" class="form-control" required>
                </div>
                <div class="col">
                    <input type="text" placeholder="Nombre de Usuario" name="username" class="form-control" required>
                </div>
            </div>
            <div>
                <input type="email" placeholder="Correo Electronico" name="email" class="form-control" required>
            </div>
            <div>
                <input type="password" placeholder="Contraseña" name="password" class="form-control" required>
            </div>
            <button class="btn btn-dark btn-lg">Dar de alta</button>
        </form>
    </div>
</template>
<script>
export default {
    name: "LoginForm",
    props: ["registrar"],
    methods: {
        handleRegister(e) {
            e.preventDefault()
            let $form = e.target
            let usuarioFinal = {
                name: $form.name.value,
                username: $form.username.value,
                email: $form.email.value,
                password: $form.password.value
            }
            this.registrar(usuarioFinal)
        }
    }
}

</script>

<style>
#form-register {
    height: 80%;
}
</style>