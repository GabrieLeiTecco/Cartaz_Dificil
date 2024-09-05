<script>
export default {
    name: 'SistemaQueArrasta',
    data: function () {
        return {
            positions: {
                clientX: undefined,
                clientY: undefined,
                movementX: 0,
                movementY: 0
            }
        }
    },
    methods: {
        arrastar: function (event) {
            event.preventDefault()
            this.positions.clientX = event.clientX
            this.positions.clientY = event.clientY
            document.onmousemove = this.mexerElemento
            document.onmouseup = this.pararMexerElemento
        },
        mexerElemento: function(event){
            event.preventDefault()
            this.positions.movementX = this.positions.clientX - event.clientX
            this.positions.movementY = this.positions.clientY - event.clientY
            this.positions.clientX = event.clientX
            this.positions.clientY = event.clientY
            this.$refs.divPrincipal.style.top = (this.$refs.divPrincipal.offsetTop - this.positions.movementY) + 'px'
            this.$refs.divPrincipal.style.left = (this.$refs.divPrincipal.offsetLeft - this.positions.movementX) + 'px'
        },
        pararMexerElemento: function(){
            document.onmouseup = false
            document.onmousemove = false
        },
        naoMove: function(){
            alert('Não move!')
        }
    }
}
</script>

<template>
    <div ref="divPrincipal" id="divPrincipal">
        <div id="divMove" @mousedown="arrastar">
            <h1>DA PARA MOVER</h1>
        </div>
        <div id="divNaoMove" @mousedown="naoMove">
            <h1>NÃO DA PARA MOVER</h1>
        </div>
    </div>
</template>
 
<style>
#divPrincipal {
  position: absolute;
  z-index: 9;
}
#divMove {
  cursor: grab;
  z-index: 10;
}
</style>