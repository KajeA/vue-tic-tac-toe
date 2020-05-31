<template>
  
</template>

<script>
    export default {
        data () {}
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