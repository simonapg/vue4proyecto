<template>
  <section class="modulo">
    <div class="modulo-header">
      <h2>2. Tarjetas Clicables</h2>
      <span class="badge">@click @click.stop @click.capture</span>
    </div>
    
    <div 
      @click="logBubbling('contenedor')"
      @click.capture="logCaptura"
    >
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Titulo</th>
            <th>Descripcion</th>
            <th>Estado</th>
            <th>Accion</th>
          </tr>
        </thead>
        <tbody>
          <tr 
            v-for="tarjeta in tarjetas" 
            :key="tarjeta.id"
            :class="{ 'seleccionada': tarjeta.seleccionada }"
            @click="seleccionarTarjeta(tarjeta.id)"
          >
            <td>{{ tarjeta.id }}</td>
            <td>{{ tarjeta.titulo }}</td>
            <td>{{ tarjeta.descripcion }}</td>
            <td>
              <span v-if="tarjeta.seleccionada">[SELECCIONADA]</span>
              <span v-if="tarjeta.favorita"> [FAVORITA]</span>
            </td>
            <td>
              <button 
                @click.stop="marcarFavorito(tarjeta.id)"
                class="btn btn-sm"
                :style="{ 
                  background: tarjeta.favorita ? 'var(--color-black)' : 'var(--color-white)', 
                  color: tarjeta.favorita ? 'var(--color-white)' : 'var(--color-black)' 
                }"
              >
                {{ tarjeta.favorita ? 'Quitar' : 'Favorito' }}
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div v-if="tarjetaSeleccionadaId" style="margin-top: var(--spacing-lg); padding: var(--spacing-md); border: 1px solid var(--color-gray-medium); background: var(--color-gray-light);">
      <strong>Seleccionada:</strong> {{ obtenerTarjetaSeleccionada() }}
    </div>
  </section>
</template>

<script>
export default {
  name: 'TarjetasClicables',
  emits: ['registrar-evento'],
  data() {
    return {
      tarjetas: [
        { 
          id: 1, 
          titulo: 'Vue.js Essentials', 
          descripcion: 'Fundamentos de Vue 3', 
          seleccionada: false, 
          favorita: false 
        },
        { 
          id: 2, 
          titulo: 'Event Modifiers', 
          descripcion: 'Modificadores: .stop, .prevent, .once', 
          seleccionada: false, 
          favorita: false 
        },
        { 
          id: 3, 
          titulo: 'Event Bubbling', 
          descripcion: 'Propagacion y .capture', 
          seleccionada: false, 
          favorita: false 
        },
        { 
          id: 4, 
          titulo: 'Key Modifiers', 
          descripcion: 'Modificadores: .enter, .esc, .ctrl', 
          seleccionada: false, 
          favorita: false 
        },
      ],
      tarjetaSeleccionadaId: null
    }
  },
  methods: {
    seleccionarTarjeta(id) {
      this.tarjetas.forEach(t => t.seleccionada = false)
      
      const tarjeta = this.tarjetas.find(t => t.id === id)
      if (tarjeta) {
        tarjeta.seleccionada = true
        this.tarjetaSeleccionadaId = id
        this.$emit('registrar-evento', {
          tipo: 'tarjeta',
          mensaje: `Tarjeta ${id} seleccionada: "${tarjeta.titulo}" (@click)`
        })
      }
    },
    
    marcarFavorito(id) {
      const tarjeta = this.tarjetas.find(t => t.id === id)
      if (tarjeta) {
        tarjeta.favorita = !tarjeta.favorita
        const accion = tarjeta.favorita ? 'marcada como favorita' : 'removida de favoritos'
        this.$emit('registrar-evento', {
          tipo: 'favorito',
          mensaje: `Tarjeta ${id} ${accion} (@click.stop)`
        })
      }
    },
    
    logCaptura() {
      this.$emit('registrar-evento', {
        tipo: 'capture',
        mensaje: 'Evento capturado en contenedor (@click.capture) - Fase de captura'
      })
    },
    
    logBubbling(elemento) {
      this.$emit('registrar-evento', {
        tipo: 'bubbling',
        mensaje: `Click en ${elemento} - Fase de bubbling`
      })
    },
    
    obtenerTarjetaSeleccionada() {
      const tarjeta = this.tarjetas.find(t => t.id === this.tarjetaSeleccionadaId)
      return tarjeta ? `${tarjeta.id} - ${tarjeta.titulo}` : ''
    }
  }
}
</script>

<style scoped>
table {
  font-size: var(--font-size-sm);
}

td button {
  padding: 4px 8px;
  font-size: 12px;
}
</style>
