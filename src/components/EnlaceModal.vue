<template>
  <section class="modulo">
    <div class="modulo-header">
      <h2>5. Enlace que NO Navega</h2>
      <span class="badge">@click.prevent @click.stop</span>
    </div>
    
    <p>El siguiente enlace usa <code>@click.prevent</code> para prevenir la navegación:</p>
    
    <a 
      href="https://google.cl" 
      @click.prevent="abrirModal"
      class="link-action"
    >
      Click aquí - No navegará
    </a>
    
    <div v-if="modalAbierto" class="modal-overlay" @click="cerrarModal">
      <div class="modal" @click.stop>
        <div class="modal-header">
          <h2>Información del Modal</h2>
          <button @click="cerrarModal" class="btn-close">×</button>
        </div>
        <div class="modal-body">
          <p>Hiciste click en un enlace que normalmente te llevaría a Google Chile, pero en lugar de navegar a esa página, se abrió este modal. Esto es útil cuando quieres interceptar el comportamiento normal de un enlace y hacer algo diferente. Si haces click fuera de este cuadro se cerrará, pero si haces click dentro no pasa nada porque así está configurado.</p>
        </div>
        <div class="modal-footer">
          <button @click="cerrarModal" class="btn btn-primary">Cerrar Modal</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'EnlaceModal',
  emits: ['registrar-evento'],
  data() {
    return {
      modalAbierto: false
    }
  },
  methods: {
    abrirModal() {
      this.modalAbierto = true
      this.$emit('registrar-evento', {
        tipo: 'modal',
        mensaje: 'Modal abierto con @click.prevent - Navegación bloqueada'
      })
    },
    
    cerrarModal() {
      this.modalAbierto = false
      this.$emit('registrar-evento', {
        tipo: 'modal',
        mensaje: 'Modal cerrado con @click.stop'
      })
    }
  }
}
</script>

<style scoped>
.link-action {
  display: inline-block;
  padding: var(--spacing-md) var(--spacing-lg);
  background: var(--color-black);
  color: var(--color-white);
  text-decoration: none;
  border-radius: var(--radius-sm);
  font-weight: 500;
  cursor: pointer;
}

.link-action:hover {
  background: var(--color-gray-dark);
  text-decoration: none;
}
</style>