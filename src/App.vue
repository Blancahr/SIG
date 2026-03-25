<template>
  <div class="container">
    <h1>Sistema Interno de Gestión</h1>
    <h2>Registro de Documentos</h2>

    <form @submit.prevent="guardarDocumento">
      <div class="campo">
        <label>Folio</label>
        <input type="text" v-model="documento.folio" required />
      </div>

      <div class="campo">
        <label>Fecha</label>
        <input type="date" v-model="documento.fecha" required />
      </div>

      <div class="campo">
        <label>Tipo de documento</label>
        <input type="text" v-model="documento.tipo" required />
      </div>

      <div class="campo">
        <label>Área destino</label>
        <input type="text" v-model="documento.area" required />
      </div>

      <div class="campo">
        <label>Observaciones</label>
        <textarea v-model="documento.observaciones"></textarea>
      </div>

      <h3>Datos del Solicitante</h3>

      <div class="campo">
        <label>Nombre del solicitante</label>
        <input type="text" v-model="documento.solicitante.nombre" required />
      </div>

      <div class="campo">
        <label>Tipo de solicitante</label>
        <select v-model="documento.solicitante.tipo" required>
          <option disabled value="">Seleccione una opción</option>
          <option>Ciudadano</option>
          <option>Empresa</option>
          <option>Dependencia</option>
        </select>
      </div>

      <div class="campo">
        <label>Contacto</label>
        <input type="text" v-model="documento.solicitante.contacto" />
      </div>

      <button type="submit">Guardar documento</button>
    </form>

    <hr />

<TablaDocumentos :documentos="documentos" />

<hr />

<Reportes :documentos="documentos" />

<hr />

<Usuarios />

  </div>
</template>




<script>
import Usuarios from './components/Usuarios.vue'
import Reportes from './components/Reportes.vue'
import TablaDocumentos from './components/TablaDocumentos.vue'

export default {
  name: 'App',

  components: {
    Usuarios,
    Reportes,
    TablaDocumentos
  },

  data() {
    return {
      documento: {
        folio: '',
        fecha: '',
        tipo: '',
        area: '',
        observaciones: '',
        solicitante: {
          nombre: '',
          tipo: '',
          contacto: ''
        }
      },

      documentos: [
        { id: "SIG-001", nombre: "Oficio A", estado: "Recibido" },
        { id: "SIG-002", nombre: "Reporte", estado: "En proceso" }
      ]
    }
  },

  methods: {
    guardarDocumento() {
      if (!this.documento.folio || !this.documento.tipo) {
        alert("Faltan campos obligatorios")
        return
      }

      this.documentos.push({
        id: this.documento.folio,
        nombre: this.documento.tipo,
        estado: "Recibido"
      })

      console.log('Documento registrado:', this.documento)
      alert('Documento registrado correctamente')
      this.limpiarFormulario()
    },

    limpiarFormulario() {
      this.documento = {
        folio: '',
        fecha: '',
        tipo: '',
        area: '',
        observaciones: '',
        solicitante: {
          nombre: '',
          tipo: '',
          contacto: ''
        }
      }
    }
  }
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}

.campo {
  margin-bottom: 15px;
}

label {
  display: block;
  font-weight: bold;
}

input,
textarea {
  width: 100%;
  padding: 6px;
}

button {
  padding: 8px 16px;
}
</style>