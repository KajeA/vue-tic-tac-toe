<template>
  <table class="grid">
  	<tr>
  		<cell name="1"></cell>
			<cell name="2"></cell>
			<cell name="3"></cell>
  	</tr>
		<tr>
			<cell name="4"></cell>
			<cell name="5"></cell>
			<cell name="6"></cell>
		</tr>
		<tr>
			<cell name="7"></cell>
			<cell name="8"></cell>
			<cell name="9"></cell>
		</tr>
  </table>
</template>

<script>
  export default {
    data () {
			return {
				activePlayer: 'O',

				gameStatus: 'turn',

				gameStatusMessage: `O's turn`,

				gameStatusColour: 'statusTurn',

				movesTaken: 0,
				
				cells : {
					1: '', 2: '', 3: '',
					4: '', 5: '', 6: '',
					7: '', 8: '', 9: '', 
				},

				winConditions: [
					[1, 2, 3], [4, 5, 6], [7, 8, 9],
					[1, 4, 7], [2, 5, 8], [3, 6, 9],
					[1, 5, 9], [3, 5, 7], 
				],
		}
  }
</script>

<style lang='scss'>
@import './styles/main.scss';

.grid {
  background-color: $primary;
  color: $secondary;
  width: 100%;
}

.gameStatus {
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  background-color: $secondary;
  color: $primary;
}

.statusTurn {
  background-color: $secondary;
}

.statusWin {
  background-color: green;
}

.statusDraw {
  background-color: yellow;
}

</style>