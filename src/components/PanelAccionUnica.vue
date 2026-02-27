<template>
  <section class="modulo">
    <div class="modulo-header">
      <h2>3. Panel - Acción Única</h2>
      <span class="badge">@click.once</span>
    </div>
    
    <button 
      @click.once="mostrarTips" 
      :disabled="tipsActivado"
      class="btn btn-primary btn-block"
    >
      {{ !tipsActivado ? 'Mostrar Tips (solo una vez)' : 'Tips Mostrados' }}
    </button>
    
    <div v-if="tipsActivado" class="tips-panel">
      <p>Los modificadores de eventos en Vue permiten controlar el comportamiento de los eventos del DOM sin tener que escribir código adicional en los métodos. Por ejemplo, puedes evitar que un formulario recargue la página al enviarse, o detener la propagación de un evento para que no afecte a otros elementos padres. También existen modificadores para teclas específicas como Enter o Escape que facilitan la creación de atajos de teclado en tu aplicación. Vue ofrece opciones como once para eventos que solo deben ejecutarse una única vez, y passive para mejorar el rendimiento en gestos táctiles.</p>
    </div>
  </section>
</template>

<script>
export default {
  name: 'PanelAccionUnica',
  emits: ['registrar-evento'],
  data() {
    return {
      tipsActivado: false
    }
  },
  methods: {
    mostrarTips() {
      this.tipsActivado = true
      this.$emit('registrar-evento', {
        tipo: 'once',
        mensaje: 'Tips mostrados (@click.once) - Este botón solo funciona UNA VEZ'
      })
    }
  }
}
</script>

<style scoped>
.tips-panel {
  margin-top: var(--spacing-xl);
  padding: var(--spacing-xl);
  background: var(--color-gray-light);
  border: 1px solid var(--color-gray-medium);
}

.tips-panel p {
  margin: 0;
  line-height: 1.8;
  color: var(--color-black);
}
</style>
