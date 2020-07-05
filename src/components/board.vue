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
	import cell from './cell.vue'
	import '../styles/main.scss'
	
	export default {
		components: { cell },

		data () {
			return {
				activePlayer: 'O',

				gameStatus: 'turn',

				gameStatusMessage:  `O's Turn`,

				gameStatusColour: 'statusTurn',

				movesTaken: 0,
				
				cells : {
					1: '', 2: '', 3: '',
					4: '', 5: '', 6: '',
					7: '', 8: '', 9: '' 
				},

				winConditions: [
					[1, 2, 3], [4, 5, 6], [7, 8, 9],
					[1, 4, 7], [2, 5, 8], [3, 6, 9],
					[1, 5, 9], [3, 5, 7]
				],
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

				return
			} else if (this.gameStatus === 'draw') {
				this.gameStatusColour = 'statusDraw'

				this.gameStatusMessage = 'Draw!'

				return
			} 
				
		}
	},

	methods: {
		changePlayer () {
			this.activePlayer = this.nonActivePlayer

			if (this.gameStatus === 'turn') {
				this.gameStatusMessage = `${this.activePlayer}'s turn`
			}
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

		gameIsWon () {
			Event.$emit('win', this.activePlayer)

				this.gameStatusMessage = `${this.activePlayer} Wins!`

				Event.$emit('freeze')

			return 'win'
		},

		changeGameStatus () {
			if (this.checkForWin()) {
				return this.gameIsWon()
			} else if (this.movesTaken === 9) {
				return 'draw'
			}
			return 'turn'
		},

		areEqual () {
			var length = arguments.length;

			for (var i = 1; i < length; i++){
				if (arguments[i] === '' || arguments[i] !== arguments[i-1])
					return false;
			}
			return true;
		},
	},

	created () {
		Event.$on('strike', (cellNumber) => {
			this.cells[cellNumber] = this.activePlayer

			this.movesTaken++

			this.gameStatus = this.changeGameStatus()

			this.changePlayer()
		})
		Event.$on('boardReset', () => {
			Object.assign(this.$data, this.$options.data())
		})
	},
  }
</script>

<style lang='scss'>
@import '../styles/_variables.scss';

.grid {
  background-color: $primary;
  color: $secondary;
  width: 100%;
}

.gameStatus {
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  background-color: $secondary;
  color: $tertiary;
  font-size: 2rem;
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