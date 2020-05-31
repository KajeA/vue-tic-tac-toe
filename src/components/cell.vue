<template>

</template>

<script>
    export default {
        data () {}
    }
</script>

<style lang="scss">

.cell {
    width: 33.333%;
    height: 4em;
    border: 0.5em solid $primary;
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
        border-left-color: transparent;
        border-top-color: transparent;
    }
    &:nth-of-type(2) {
        border-top-color: transparent;
    }
    &:nth-of-type(3) {
        border-right-color: transparent;
        border-top-color: transparent;
    }
}

tr:nth-of-type(3) .cell {
    border-bottom-color: transparent;
}
</style>