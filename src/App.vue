<template>
  <div id='app'>
    <div id="details">
      <h1>Tic Tac Toe</h1>
    </div>

    <grid></grid>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      matches: 0,
      wins: {
        O: 0,
        X: 0
      }
    }
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
    color: $primary;
    @extend .btn;
    &:hover {
      color: $secondary;
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
