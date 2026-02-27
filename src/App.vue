<template>
  <div id="app">
    <header class="app-header">
      <h1>Centro de Eventos - Vue 3</h1>
      <p>Demostración de eventos DOM, modificadores y manejadores</p>
    </header>
    
    <div class="grid-2col">
      <FormularioBusqueda @registrar-evento="registrarEvento" />
      <TarjetasClicables @registrar-evento="registrarEvento" />
      <PanelAccionUnica @registrar-evento="registrarEvento" />
      <CajaScrollable @registrar-evento="registrarEvento" />
      <EnlaceModal @registrar-evento="registrarEvento" />
      <RegistroEventos 
        :eventos="registroEventos" 
        :maxEventos="maxEventos"
        @limpiar="limpiarRegistro"
      />
    </div>
    
    <footer class="app-footer">
      <p>Centro de Eventos - Vue 3 | Demostración de modificadores de eventos</p>
    </footer>
  </div>
</template>

<script>
import FormularioBusqueda from './components/FormularioBusqueda.vue'
import TarjetasClicables from './components/TarjetasClicables.vue'
import PanelAccionUnica from './components/PanelAccionUnica.vue'
import CajaScrollable from './components/CajaScrollable.vue'
import EnlaceModal from './components/EnlaceModal.vue'
import RegistroEventos from './components/RegistroEventos.vue'

export default {
  name: 'App',
  components: {
    FormularioBusqueda,
    TarjetasClicables,
    PanelAccionUnica,
    CajaScrollable,
    EnlaceModal,
    RegistroEventos
  },
  data() {
    return {
      registroEventos: [],
      maxEventos: 20,
      eventoIdCounter: 0
    }
  },
  methods: {
    registrarEvento(evento) {
      const timestamp = new Date().toLocaleTimeString('es-ES')
      
      this.registroEventos.unshift({
        id: ++this.eventoIdCounter,
        tipo: evento.tipo,
        timestamp,
        mensaje: evento.mensaje
      })
      
      if (this.registroEventos.length > this.maxEventos) {
        this.registroEventos.pop()
      }
    },
    
    limpiarRegistro() {
      const cantidadEventos = this.registroEventos.length
      this.registroEventos = []
      this.registrarEvento({
        tipo: 'sistema',
        mensaje: `Registro limpiado (${cantidadEventos} eventos eliminados)`
      })
    }
  },
  mounted() {
    this.registrarEvento({
      tipo: 'sistema',
      mensaje: 'Centro de Eventos iniciado - Aplicación lista'
    })
  }
}
</script>
