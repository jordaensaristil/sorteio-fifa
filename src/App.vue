<template>
  <div class="container app-home d-flex flex-column align-items-center justify-content-center min-vh-100">
    <h1 class="mb-4 text-white fw-bold">🎮 FIFA Sorteio App</h1>
    <div class="row g-4">
      <div class="col-md-6">
        <div class="card card-menu shadow-lg" @click="tela = 'sorteio'">
          <img src="https://cdn-icons-png.flaticon.com/512/861/861512.png" class="card-img-top p-4" alt="Sorteio" />
          <div class="card-body text-center">
            <h4 class="card-title fw-bold">⚽ Sortear Times</h4>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <div class="card card-menu shadow-lg" @click="tela = 'campeonato'">
          <img src="https://cdn-icons-png.flaticon.com/512/841/841364.png" class="card-img-top p-4" alt="Campeonato" />
          <div class="card-body text-center">
            <h4 class="card-title fw-bold">🏆 Montar Campeonato</h4>
          </div>
        </div>
      </div>
    </div>

    <SorteioTimes v-if="tela === 'sorteio'" @voltar="tela = ''" />
    <CampeonatoFifa v-if="tela === 'campeonato'" @voltar="tela = ''" />
  </div>
</template>

<script>
import SorteioTimes from './SorteioTimes.vue'
import CampeonatoFifa from './CampeonatoFifa.vue'

export default {
  components: { SorteioTimes, CampeonatoFifa },
  data() {
    return {
      tela: ''
    }
  }
}
</script>

<style>
body {
  background: linear-gradient(120deg, #0d1b2a, #1b263b);
  font-family: 'Segoe UI', sans-serif;
}

.app-home h1 {
  color: #fff;
  text-shadow: 1px 1px 8px rgba(255,255,255,0.3);
}

.card-menu {
  background-color: #ffffff12;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.card-menu:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 30px rgba(255, 255, 255, 0.2);
}
.card-menu img {
  height: 100px;
  object-fit: contain;
}
.card-title {
  color: white;
}
</style>
