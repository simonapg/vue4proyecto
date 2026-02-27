<template>
  <section class="modulo">
    <div class="modulo-header">
      <h2>6. Registro de Eventos (Audit Log)</h2>
      <span class="badge">Real-time event tracking</span>
    </div>
    
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: var(--spacing-lg); padding-bottom: var(--spacing-md); border-bottom: 1px solid var(--color-gray-medium);">
      <div><strong>{{ eventos.length }} / {{ maxEventos }} eventos</strong></div>
      <button @click="limpiarRegistro" class="btn btn-sm">Limpiar Registro</button>
    </div>
    
    <div class="audit-log">
      <div 
        v-for="evento in eventos" 
        :key="evento.id"
        class="evento-item"
      >
        {{ evento.timestamp }} - {{ evento.mensaje }}
      </div>
      
      <div v-if="eventos.length === 0" class="sin-eventos">
        No hay eventos registrados. Interactua con los modulos para ver eventos aqui.
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'RegistroEventos',
  props: {
    eventos: {
      type: Array,
      default: () => []
    },
    maxEventos: {
      type: Number,
      default: 20
    }
  },
  emits: ['limpiar'],
  methods: {
    limpiarRegistro() {
      this.$emit('limpiar')
    }
  }
}
</script>

<style scoped>
.audit-log {
  max-height: 400px;
  overflow-y: auto;
  background: var(--color-white);
  border: 1px solid var(--color-gray-medium);
  padding: var(--spacing-lg);
}

.evento-item {
  padding: var(--spacing-sm) 0;
  font-size: var(--font-size-sm);
  line-height: 1.6;
  color: var(--color-black);
}

.sin-eventos {
  padding: var(--spacing-xl);
  text-align: center;
  color: var(--color-gray-dark);
  font-size: var(--font-size-sm);
}
</style>
