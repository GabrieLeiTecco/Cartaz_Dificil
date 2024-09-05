<template>
    <div ref="elementoQueMove" id="draggable-container"> <!-- ref é tipo um ID -->
      <div id="draggable-header" @mousedown="arrastarMouse"> <!-- MOusedown é o evento do mouse sendo pressionado dentro do elemento -->
        <h1>TEXTO</h1>
      </div>
      <div>
        <h1>OUTRO TEXTO</h1>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'DivQueArrasta',
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
      arrastarMouse: function (event) {
        event.preventDefault() // para a função padrão do elemento, fazendo parar de selecionar o texto e pa
        this.positions.clientX = event.clientX // pega as posições iniciais do elemento
        this.positions.clientY = event.clientY
        document.onmousemove = this.mexerElemento // quando o mouse mexer no documento ele executa a função
        document.onmouseup = this.paraMexerElemento // quando parar de pressionar o mouse ele executa a função
      },
      mexerElemento: function (event) {
        event.preventDefault()
        this.positions.movementX = this.positions.clientX - event.clientX
        this.positions.movementY = this.positions.clientY - event.clientY
        this.positions.clientX = event.clientX
        this.positions.clientY = event.clientY
        // coloca no novo posicionamento o elemento
        this.$refs.elementoQueMove.style.top = (this.$refs.elementoQueMove.offsetTop - this.positions.movementY) + 'px'
        this.$refs.elementoQueMove.style.left = (this.$refs.elementoQueMove.offsetLeft - this.positions.movementX) + 'px'
      },
      paraMexerElemento () {
        document.onmouseup = false
        document.onmousemove = false
      }
    }
  }
  </script>
  
  <style>
  #draggable-container {
    position: absolute;
    z-index: 9;
  }
  #draggable-header {
    cursor: grab;
    z-index: 10;
  }
  </style>
  