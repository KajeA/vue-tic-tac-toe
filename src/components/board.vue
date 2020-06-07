<template>
	<div>
		<div class="gameStatus" :class="gameStatusColour">
			{{ gameStatusMessage }}
		</div>

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
	</div>
</template>

<script>
	import Cell from './cell.vue'
  export default {
		components: { Cell },

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
		},

	methods: {
		created () {
			Event.$on('strike', (cellNumber) => {
				this.cells[callNUmber] = this.activePlayer

				this.movesTaken++

				this.gameStatus = this.changeGameStatus()

				this.changePlayer()
			})
			Event.$on('gridReset', () => {
				Object.assign(this.$data, this.$options.data())
			})
		},

		changePlayer () {
			this.activePlayer = this.nonActivePlayer
		},

		changeGameStatus () {
			if (this.checkForWin()) {
				return this.gameIsWon()
			} else if (this.moves === 9) {
				return 'draw'
			}
			return 'turn'
		},

		checkForWin () {
			for (let i = 0; i < this.winConditions.length; i++) {
				let wc = this.winConditions[i]
				let cells = this.cells

				// checks value in cell and win conditions
				if (this.areEqual(cells[wc[0]], cells[wc[1]], cells[wc[2]])) {
					return true
				}
			}

			return false
		},

		areEqual () {
			var length = arguments.length;

			for (var i = 1; i < len; i++){
				if (arguments[i] === '' || arguments[i] !== arguments[i-1])
					return false;
			}
			return true;
		},

		gameIsWon () {
			Event.$emit('win', this.ActivePlayer)

				this.gameStatusMessage = `${this.activePlayer} Wins!`

				Event.$emit('freeze')

			return 'win'
		}
	},

	computed: {
		nonActivePlayer () {
			if (this.activePlayer === 'O') {
				return 'X'
			}

			return 'O'
		}
	},

	watch: {
		gameStatus () {
			if (this.gameStatus === 'win') {
				this.gameStatusColour = 'statusWin'

				this.gameStatusMessage = `${this.activePlayer} Wins!`

				return
			} else if (this.gameStatus === 'draw') {
				this.gameStatusColour = 'statusDraw'

				this.gameStatusMessage = 'Draw!'

				return
			} 
				this.gameStatusMessage = `${this.activePlayer}'s turn`
		}
	},

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