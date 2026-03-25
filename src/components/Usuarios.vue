<template>
  <div>
    <h2>Gestión de Usuarios</h2>

    <input v-model="nombre" placeholder="Nombre" />
    <input v-model="correo" placeholder="Correo" />

    <button @click="agregarUsuario">Agregar</button>

    <ul>
      <li v-for="user in usuarios" :key="user.id">
        {{ user.nombre }} - {{ user.correo }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      correo: '',
      usuarios: []
    }
  },
  methods: {
    agregarUsuario() {
      if (!this.nombre || !this.correo) {
        alert("Completa los campos")
        return
      }

      this.usuarios.push({
        id: Date.now(),
        nombre: this.nombre,
        correo: this.correo
      })

      this.nombre = ''
      this.correo = ''
    }
  }
}
</script>