<template>
  <section class="modulo">
    <div class="modulo-header">
      <h2>4. Caja Scrollable</h2>
      <span class="badge">@scroll.passive</span>
    </div>
    
    <div class="scroll-wrapper">
      <div 
        class="scroll-container" 
        @scroll.passive="onScroll"
      >
        <div v-for="n in 40" :key="n" class="scroll-item">
          Elemento {{ n }}
        </div>
      </div>
      
      <div class="scroll-indicator-track">
        <div class="scroll-indicator-box" :style="{ top: scrollPercentage + '%' }"></div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'CajaScrollable',
  emits: ['registrar-evento'],
  data() {
    return {
      scrollPosition: 0,
      scrollPercentage: 0
    }
  },
  methods: {
    onScroll(event) {
      const elemento = event.target
      this.scrollPosition = Math.round(elemento.scrollTop)
      
      const scrollHeight = elemento.scrollHeight - elemento.clientHeight
      this.scrollPercentage = scrollHeight > 0 
        ? Math.round((elemento.scrollTop / scrollHeight) * 100) 
        : 0
      
      if (this.scrollPosition % 100 === 0 || this.scrollPosition < 10) {
        this.$emit('registrar-evento', {
          tipo: 'scroll',
          mensaje: `Scroll: ${this.scrollPercentage}% - @scroll.passive`
        })
      }
    }
  }
}
</script>

<style scoped>
.scroll-wrapper {
  display: flex;
  gap: var(--spacing-md);
}

.scroll-container {
  flex: 1;
  height: 200px;
  overflow-y: auto;
  border: 1px solid var(--color-gray-medium);
  background: var(--color-white);
}

.scroll-item {
  padding: var(--spacing-md);
  border-bottom: 1px solid var(--color-gray-medium);
  font-size: var(--font-size-sm);
}

.scroll-indicator-track {
  width: 30px;
  height: 200px;
  background: var(--color-gray-light);
  border: 1px solid var(--color-gray-medium);
  position: relative;
}

.scroll-indicator-box {
  width: 20px;
  height: 20px;
  background: var(--color-black);
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: top 0.1s ease-out;
}
</style>
