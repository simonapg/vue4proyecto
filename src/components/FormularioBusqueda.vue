<template>
  <section class="modulo">
    <div class="modulo-header">
      <h2>1. Formulario - Búsqueda</h2>
      <span class="badge">@submit.prevent @keyup.enter @keydown.esc</span>
    </div>

    <form @submit.prevent="buscar">
      <input 
        v-model="busqueda"
        type="text" 
        placeholder="Escribe y presiona Enter..."
        @keyup.enter="buscar"
        @keydown.esc="limpiar"
      />
      <button type="submit" class="btn btn-primary">Buscar</button>
    </form>

    <div v-if="resultados.length > 0" style="margin-top: var(--spacing-lg);">
      <p><strong>Resultados:</strong></p>
      <ul>
        <li v-for="resultado in resultados" :key="resultado">{{ resultado }}</li>
      </ul>
    </div>

    <div v-else style="color: var(--color-gray-dark); font-size: var(--font-size-sm); margin-top: var(--spacing-lg);">
      <p>Presiona Enter o haz clic en Buscar</p>
      <p>Presiona Esc para limpiar</p>
    </div>
  </section>
</template>

<script>
export default {
  name: 'FormularioBusqueda',
  emits: ['registrar-evento'],
  data() {
    return {
      busqueda: '',
      resultados: []
    }
  },
  methods: {
    buscar() {
      if (this.busqueda.trim()) {
        this.resultados = [
          `Resultado 1: "${this.busqueda}"`,
          `Resultado 2: "${this.busqueda}" coincide`,
          `Resultado 3: "${this.busqueda}" encontrado`
        ]
        this.$emit('registrar-evento', {
          tipo: 'buscar',
          mensaje: `Búsqueda realizada: "${this.busqueda}" (@submit.prevent)`
        })
      }
    },
    
    limpiar() {
      this.busqueda = ''
      this.resultados = []
      this.$emit('registrar-evento', {
        tipo: 'buscar',
        mensaje: `Búsqueda limpiada (@keydown.esc)`
      })
    }
  }
}
</script>

<style scoped>
form input {
  flex: 1;
  min-width: 200px;
}
</style>
