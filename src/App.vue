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
    <LogList :logs="logs"/>
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
    game: false,
    winner: null,
    healthPlayer: 0,
    healthMonster: 0,
    namePlayer: "",
  }),
  watch: {
    healthPlayer(value){
      if (value <= 0) {
        this.winner = "Monster";
        this.game = false;
      }
    },
    healthMonster(value){
      if (value <= 0) {
        this.winner = this.namePlayer;
        this.game = false;
      }
    },
  },
  methods: {
    hp(){
      this.logs.unshift({player: "Player",
      action: "health",
      value: this.healthPlayer
      });
    },
    setGame(value){
      this.game = value;
      this.healthPlayer = 100;
      this.healthMonster = 100;
      this.logs = [];
      this.namePlayer = "DS";
    },
    getRandom(min, max){
      const val = Math.floor(Math.random() * (max-min)) + min;
      return val;
    },
    atackToMonster(){
      const value = this.getRandom(6,10);
      this.healthMonster -= value;
      this.logs.unshift({player: this.namePlayer,
      action: "atack",
      value
      });
      this.atackToPlayer();
    },
    atackToPlayer(){
      const value = this.getRandom(8,12);
      this.healthPlayer -= value;
      this.logs.unshift({player: "Monster",
      action: "atack",
      value
      });
    },
    superAtackToMonster(){
      const value = this.getRandom(10,14);
      this.healthMonster -= value;
      this.logs.unshift({player: this.namePlayer,
      action: "atack",
      value
      });
      this.atackToPlayer();
    },
    heal(){
      const value = this.getRandom(6,10);
      this.healthPlayer += value;
      this.logs.unshift({player: this.namePlayer,
      action: "heal yourself",
      value
      });
      this.atackToPlayer();
    },
    surrender(){
      this.logs.unshift({player: "Player",
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
