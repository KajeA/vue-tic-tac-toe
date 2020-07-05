<template>
	<td class="cell" @click="strike">{{ mark }}</td>
</template>

<script>
  import '../styles/main.scss'

  export default {
		props: ['name'],
    data () {
			return {
				frozen: false, // prevents player from changing placement

				mark: ''
			}
		},
		methods: {
			strike () {
				if (! this.frozen) {
					this.mark = this.$parent.activePlayer // gets x or o

					this.frozen = true

					Event.$emit('strike', this.name) // notifies board that mark is placed
				}
      }
    },
    
    created () {
      Event.$on('clearCell', () => {
        this.mark = ''

        this.frozen = false
      })

      Event.$on('freeze', () => this.frozen = true)
    }
  }
</script>

<style lang="scss">
@import '../styles/_variables.scss';

.cell {
  width: 33.333%;
  height: 4em;
  border: 3px solid $border;
  font-size: 3em;
  font-family: $font-secondary;
  &:hover {
      background-color: pink;
  }
  &::after {
      content: '';
      display: block;
  }
  &:first-of-type {
      border-left-color: $border;
      border-top-color: $border;
  }
  &:nth-of-type(2) {
      border-top-color: $border;
  }
  &:nth-of-type(3) {
      border-right-color: $border;
      border-top-color: $border;
  }
}

tr:nth-of-type(3) .cell {
  border-bottom-color: $border;
}
</style>