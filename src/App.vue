<template>
  <div>
    <div class="scoreBoard">
      <h1>Tic Tac Toe</h1>
      <h2>Score Board</h2>
      <span>O has {{ wins.O }} wins ~~~ </span> <span>X has {{ wins.X }} wins</span>
    </div>

    <div id='app'>
      <div id="details">
        <h3>{{gameType}} Match #{{ matches + 1 }}</h3> 
      </div>

      <board></board>

      <button class="restart btn" @click="restart">Restart</button>
      <!-- <button class="type btn" @click="changeGameType">Change Mode</button> -->
    </div>
  </div>
</template>

<script>
import Board from './components/board.vue'

export default {
  components: { Board },
  name: 'app',
  data () {
    return {
      gameType: 'Double',
      matches: 0,
      wins: {
        O: 0,
        X: 0
      }
    }
  },

  methods: {
    restart () {
      Event.$emit('clearCell')

      Event.$emit('boardReset')

      this.matches++
    },

    changeGameType () {
      if (this.gameType == 'Double') {
        this.gameType == 'Solo'
        
        return

      } else if (this.gameType == 'Solo') {
        this.gameType == 'Double'

        return
      }
    }
  },

  created () {
    Event.$on('win', winner => this.wins[winner]++)
  }
}
</script>

<style lang='scss'>
@import './styles/main.scss';


  body {
    background: $tertiary;
    color: $primary;
    font-family: $font-primary;
    text-align: center;
    margin: 0;
  }
  
  #app {
    margin: 0 auto;
    max-width: 30em;
    color: $primary;
  }


  // Buttons

  .restart.btn {
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    background-color: $secondary;
    color: $tertiary;
    @extend .btn;
    &:hover {
      color: $secondary;
      background-color: $tertiary;
    }
  }

  // Board

  .board {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    width: 100%;
    height: 2em;
    background-color: $primary;
    overflow-x: none;
    padding: 1em;
      h2 {
        margin: 0;
      }
      span {
        float: right;
        font-size: 1.5em;
        font-weight: 700;
        margin-left: 2em;
      }
  }
</style>
