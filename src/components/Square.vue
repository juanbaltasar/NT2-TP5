<template>
    <div :id="this.Id" class="Square" :class="this.class" :style="style" @click="SquareClick(item.Id)"></div>
</template>

<script>

  export default  {
    name: 'Square',
    props: ['item'],

    data() {
        return {
            
        }
    },

    computed: {
        style() {
            return `
            background-color:${this.item.Color};`
        },

        Id() {
            return "Square" + this.item.Id;
        },

        class(){
            let clicked = this.item.clicked;
            let Victory = this.item.Victory
            return {hidden: (clicked && !Victory)}
        }

    },

    methods: {
        SquareClick(IdSquare) {
            this.$emit('squareClick', {IdSquare})
        },
    }
}


</script>

<style scoped lang="css">
  .square {

  }
</style>
