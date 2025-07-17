<template>
  <div>
    <button @click="$emit('voltar')" class="btn btn-link mb-4">← Voltar ao Menu</button>
    <h3 class="fw-bold">Montar Campeonato FIFA (em breve)</h3>
    <p>Funcionalidade para montar campeonato será implementada aqui.</p>
  </div>
</template>

<script>
export default {
  emits: ['voltar']
};
</script>
