<template>
    <main>
        <div class="table-responsive">
            <table class="table align-middle table-dark" id="tabla-usuarios">
                <thead>
                    <tr>
                        <th>#</th>
                        <th>Nombre</th>
                        <th>Usuario</th>
                        <th>Email</th>
                        <th>Avatar</th>
                        <th>Acciones</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="usuario in usuarios" :key="usuario.id">
                        <td class="fw-bolder id-usuario">{{ usuario.id }}</td>
                        <td class="nombre-usuario">{{ usuario.name }}</td>
                        <td class="username-usuario">{{ usuario.username }}</td>
                        <td class="email-usuario">{{ usuario.email }}</td>
                        <td class="avatar-usuario"><img :src=usuario.avatar alt="imagen-usuario" />
                        </td>
                        <td><a href="#/agregar-usuario" class="text-light" @click="handleEdit"><button
                                    class="btn btn-primary mx-2 boton-editar">Editar</button></a><button
                                class="btn btn-danger" :data-id=usuario.id id="delete-user"
                                @click="handleDelete">Eliminar</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>
</template>

<script>
export default {
    name: "TablaDeUsuarios",
    props: ["usuarios", "actualizarUsuarioSeleccionado", "borrar"],
    methods: {
        handleEdit(e) {
            let $tr = e.target.closest("tr")
            let idUsuario = $tr.querySelector(".id-usuario").innerText
            let nombreUsuario = $tr.querySelector(".nombre-usuario").innerText
            let usernameUsuario = $tr.querySelector(".username-usuario").innerText
            let emailUsuario = $tr.querySelector(".email-usuario").innerText
            let avatarUsuario = $tr.querySelector(".avatar-usuario img").src

            let usuarioFinal = {
                idSeleccionado: idUsuario,
                name: nombreUsuario,
                username: usernameUsuario,
                email: emailUsuario,
                avatar: avatarUsuario
            }
            this.actualizarUsuarioSeleccionado(usuarioFinal)

        },
        handleDelete(e) {
            let respuestaUsuario = confirm("¿Estas seguro de borrar a este usuario?")
            if (respuestaUsuario) {
                let idUsuarioABorrar = e.target.dataset.id
                this.borrar(idUsuarioABorrar)
            }
        }

    }
}

</script>