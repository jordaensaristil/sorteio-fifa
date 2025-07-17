<template>
  <div class="container py-4">
    <h2 class="text-center mb-4 text-primary">🎮 Sorteio de Times</h2>

    <!-- Campo para adicionar jogador -->
    <div class="input-group mb-3">
      <input
        v-model="novoJogador"
        class="form-control"
        placeholder="Digite o nome do jogador"
        @keyup.enter="adicionarJogador"
      />
      <button
        class="btn btn-primary"
        @click="adicionarJogador"
        :disabled="!novoJogador"
      >
        Adicionar
      </button>
    </div>

    <!-- Lista de jogadores adicionados -->
    <ul class="list-group mb-3" v-if="jogadores.length">
      <li
        v-for="(j, index) in jogadores"
        :key="index"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        {{ j.nome }}
        <button class="btn btn-sm btn-danger" @click="removerJogador(index)">Remover</button>
      </li>
    </ul>

    <!-- Botão de sortear -->
    <button
      class="btn btn-success mb-4 w-100"
      @click="sortearTimes"
      :disabled="jogadores.length < 2"
    >
      🎲 Sortear Times
    </button>

    <!-- Exibir times sorteados -->
    <div class="row">
      <div class="col-md-6 mb-4" v-for="(j, index) in jogadores" :key="index">
        <div class="card h-100 shadow">
          <img
            :src="j.time?.logo || ''"
            class="card-img-top p-3"
            :alt="j.time?.nome || ''"
            style="max-height: 150px; object-fit: contain;"
          />
          <div class="card-body text-center">
            <h5 class="card-title">{{ j.nome }}</h5>
            <p class="card-text" v-if="j.time">
              <strong>{{ j.time.nome }}</strong><br />
              Liga: {{ j.time.liga }}<br />
              Pontuação: {{ j.time.pontuacao }}
            </p>
            <p v-else class="text-muted">Nenhum time sorteado ainda</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      novoJogador: '',
      jogadores: [],
      times: [
        {
          nome: 'Real Madrid',
          liga: 'La Liga',
          pontuacao: 93,
          logo: 'https://upload.wikimedia.org/wikipedia/en/5/56/Real_Madrid_CF.svg'
        },
        {
          nome: 'Manchester City',
          liga: 'Premier League',
          pontuacao: 92,
          logo: 'https://upload.wikimedia.org/wikipedia/en/e/eb/Manchester_City_FC_badge.svg'
        },
        {
          nome: 'Bayern de Munique',
          liga: 'Bundesliga',
          pontuacao: 91,
          logo: 'https://upload.wikimedia.org/wikipedia/en/1/1f/FC_Bayern_München_logo_%282017%29.svg'
        },
        {
          nome: 'Barcelona',
          liga: 'La Liga',
          pontuacao: 90,
          logo: 'https://upload.wikimedia.org/wikipedia/en/4/47/FC_Barcelona_%28crest%29.svg'
        },
        {
          nome: 'Liverpool',
          liga: 'Premier League',
          pontuacao: 89,
          logo: 'https://upload.wikimedia.org/wikipedia/en/0/0c/Liverpool_FC.svg'
        },
        {
          nome: 'PSG',
          liga: 'Ligue 1',
          pontuacao: 88,
          logo: 'https://upload.wikimedia.org/wikipedia/en/a/a7/Paris_Saint-Germain_F.C..svg'
        },
        {
          nome: 'Chelsea',
          liga: 'Premier League',
          pontuacao: 87,
          logo: 'https://upload.wikimedia.org/wikipedia/en/c/cc/Chelsea_FC.svg'
        },
        {
          nome: 'Juventus',
          liga: 'Serie A',
          pontuacao: 86,
          logo: 'https://upload.wikimedia.org/wikipedia/commons/1/15/Juventus_FC_2017_logo.svg'
        },
        {
          nome: 'Arsenal',
          liga: 'Premier League',
          pontuacao: 85,
          logo: 'https://upload.wikimedia.org/wikipedia/en/5/53/Arsenal_FC.svg'
        },
        {
          nome: 'Inter de Milão',
          liga: 'Serie A',
          pontuacao: 84,
          logo: 'https://upload.wikimedia.org/wikipedia/commons/0/05/FC_Internazionale_Milano_2021.svg'
        }
      ]
    };
  },
  methods: {
    adicionarJogador() {
      const nome = this.novoJogador.trim();
      if (nome) {
        this.jogadores.push({ nome, time: null });
        this.novoJogador = '';
      }
    },
    removerJogador(index) {
      this.jogadores.splice(index, 1);
    },
    sortearTimes() {
      if (this.jogadores.length > this.times.length) {
        alert('Número de jogadores maior que número de times disponíveis!');
        return;
      }

      const timesDisponiveis = [...this.times];
      this.jogadores = this.jogadores.map(jogador => {
        const index = Math.floor(Math.random() * timesDisponiveis.length);
        const timeSorteado = timesDisponiveis.splice(index, 1)[0];
        return {
          ...jogador,
          time: timeSorteado
        };
      });
    }
  }
};
</script>

<style scoped>
.card-img-top {
  background-color: #f8f9fa;
  border-bottom: 1px solid #ddd;
}
</style>
