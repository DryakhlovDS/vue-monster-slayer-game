<template>
  <header class="header">
    <h2>Monster slayer</h2>
  </header>
  <main>
    <section class="players">
      <PlayerBar name="Monster" :health="healthMonster" />
      <PlayerBar :name="namePlayer" :health="healthPlayer" />
    </section>
    <GameStatus v-if="!game" @newGame="setGame" :name="winner"/>
    <Actions v-else
    @atack="atackToMonster"
    @sAtack="superAtackToMonster"
    @heal="heal"
    @flag="surrender"
    />
    <LogList v-if="winner" :logs="logs"/>
  </main>
</template>

<script>
import PlayerBar from './components/PlayerBar';
import GameStatus from './components/GameStatus';
import Actions from './components/Actions';
import LogList from './components/LogList';

export default {
  name: 'App',
  components: {
    PlayerBar,
    GameStatus,
    Actions,
    LogList
  },
  data: () => ({
    logs: [],
    game: null,
    winner: null,
    healthPlayer: 0,
    healthMonster: 0,
    namePlayer: "",
    settings: {
      normal: {
        atackMin: 6,
        atackMax: 10,
        sAtackMin: 10,
        sAtackMax: 14,
        healMin: 8,
        healMax: 14,
      },
      hard: {
        atackMin: 6,
        atackMax: 8,
        sAtackMin: 10,
        sAtackMax: 12,
        healMin: 8,
        healMax: 11,
      },
    }
  }),
  watch: {
    healthPlayer(value){
      if (value <= 0) {
        this.winner = "Monster";
        this.game = null;
      }
    },
    healthMonster(value){
      if (value <= 0) {
        this.winner = this.namePlayer;
        this.game = null;
      }
    },
  },
  methods: {
    setGame(type, name){
      this.game = type;
      this.healthPlayer = 100;
      this.healthMonster = 100;
      this.logs = [];
      this.namePlayer = name;
      this.winner = "nether";
    },
    getRandom(min, max){
      const val = Math.floor(Math.random() * (max-min)) + min;
      return val;
    },
    atackToMonster(){
      const value = this.getRandom(this.settings[this.game].atackMin, this.settings[this.game].atackMax);
      this.healthMonster -= value;
      this.logs.unshift({player: this.namePlayer,
      action: "atack",
      value: value +'hp',
      });
      this.atackToPlayer();
    },
    atackToPlayer(){
      const value = this.getRandom(8,12);
      this.healthPlayer -= value;
      this.logs.unshift({player: "Monster",
      action: "atack",
      value: value +'hp',
      });
    },
    superAtackToMonster(){
      const value = this.getRandom(this.settings[this.game].sAtackMin, this.settings[this.game].sAtackMax);
      this.healthMonster -= value;
      this.logs.unshift({player: this.namePlayer,
      action: "super atack",
      value: value +'hp',
      });
      this.atackToPlayer();
    },
    heal(){
      const value = this.getRandom(this.settings[this.game].healMin, this.settings[this.game].healMax);
      this.healthPlayer += value;
      this.logs.unshift({player: this.namePlayer,
      action: "heal yourself",
      value: value +'hp',
      });
      this.atackToPlayer();
    },
    surrender(){
      this.logs.unshift({player: this.namePlayer,
      action: "surrender",
      });
      this.healthPlayer = 0;
    }
  },
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;
}

.players{
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  padding: 1.5rem;
  gap: 0.7rem
}
</style>
