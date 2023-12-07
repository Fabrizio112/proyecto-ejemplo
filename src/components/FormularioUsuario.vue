<template>
    <main>
        <form action="" id="form-users" class="my-5" @submit="onSubmit">
            <h2 class="text-center fs-2" v-if="usuarioSeleccionado.idSeleccionado.length > 0">Editar Usuario </h2>
            <h2 class="text-center fs-2" v-else>Añadir Usuario </h2>
            <div class="mb-3">
                <label class="form-label d-flex" for="nombre">Nombre</label>
                <input class="form-control" id="nombre" pattern="^[a-zA-Z ]+$" title="Solo letras y espacios en blanco"
                    v-if="usuarioSeleccionado.idSeleccionado.length > 0" required :value="usuarioSeleccionado.name">
                <input class="form-control" id="nombre" pattern="^[a-zA-Z ]+$" title="Solo letras y espacios en blanco"
                    v-else required value="">
            </div>
            <div class="mb-3">
                <label class="form-label d-flex" for="user">Usuario</label>
                <input class="form-control" id="user" title="No puede estar vacio"
                    v-if="usuarioSeleccionado.idSeleccionado.length > 0" required :value=usuarioSeleccionado.username>
                <input class="form-control" id="user" title="No puede estar vacio" v-else required value="">
            </div>
            <div class="mb-3">
                <label class="form-label d-flex" for="email">Email</label>
                <input class="form-control" id="email" pattern="^[^@]+@[^@]+\.[a-zA-Z]{2,}$"
                    title="Email incorrecto Ej: ejemplo@ejemplo.com" v-if="usuarioSeleccionado.idSeleccionado.length > 0"
                    required :value=usuarioSeleccionado.email>
                <input class="form-control" id="email" pattern="^[^@]+@[^@]+\.[a-zA-Z]{2,}$"
                    title="Email incorrecto Ej: ejemplo@ejemplo.com" v-else required value="">
            </div>
            <div class="mb-3">
                <label class="form-label d-flex" for="avatar">Avatar</label>
                <input class="form-control" id="avatar" v-if="usuarioSeleccionado.idSeleccionado.length > 0" required
                    :value=usuarioSeleccionado.avatar>
                <input class="form-control" id="avatar" v-else required value="">
            </div>
            <button class="btn btn-primary px-5 mt-3 d-flex" type="submit" :data-id=usuarioSeleccionado.idSeleccionado
                v-if="usuarioSeleccionado.idSeleccionado.length > 0">Editar</button>
            <button class="btn btn-primary px-5 mt-3 d-flex" type="submit" data-id="" v-else>Crear</button>
        </form>
    </main>
</template>
<script>
export default {
    name: "FormularioUsuario",
    props: ["editar", "agregar", "usuarioSeleccionado"],
    methods: {
        onSubmit(e) {
            e.preventDefault()
            let $form = e.target
            let $button = $form.querySelector("button")
            let usuarioFinal = {
                name: $form.nombre.value,
                username: $form.user.value,
                email: $form.email.value,
                avatar: $form.avatar.value
            }
            if (this.usuarioSeleccionado.idSeleccionado.length > 0) {
                this.editar(usuarioFinal, $button.dataset.id)
            } else {
                this.agregar(usuarioFinal)
            }
        },
        verificar() {
            console.log(this.usuarioSeleccionado.idSeleccionado.length > 0)
        }

    }
}
</script>
