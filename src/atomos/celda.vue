  <script>
  export default {
    props: {
      rowIndex: Number,
      celdaIndex: Number,
      PosicionJugador1: Object,
      PosicionJugador2: Object,
      TurnoJugador: Number,
      Bloqueoceldas: Array,
      ControldeCeldaActivado: Boolean,
      MovimientoJugador: Function,
      ControlClickCelda: Function,
      BloquearCelda: Function,
      SePuedeMover: Function,
      Marcar1: Function,
      Marcar2: Function
    },
    computed: {
      celdaClass() {
        const isjugador1 = this.PosicionJugador1.row === this.rowIndex && this.PosicionJugador1.column === this.celdaIndex;
        const isjugador2 = this.PosicionJugador2.row === this.rowIndex && this.PosicionJugador2.column === this.celdaIndex;
        const isBloqueo = this.Bloqueoceldas.some(Bloqueo => Bloqueo.row === this.rowIndex && Bloqueo.column === this.celdaIndex);
        const ismovible = (this.TurnoJugador === 1 && this.Marcar1(this.rowIndex, this.celdaIndex)) || (this.TurnoJugador === 2 && this.Marcar2(this.rowIndex, this.celdaIndex));
  
        return {
          'celda--inicio': this.rowIndex === 0 || this.rowIndex === 8,
          'celda--ColorBase': this.rowIndex != 0 && this.rowIndex != 8,
          'celda--jugador1': isjugador1,
          'celda--jugador2': isjugador2,
          'celda--deshabilitado': (this.TurnoJugador === 1 && isjugador2) || (this.TurnoJugador === 2 && isjugador1),
          'celda--movible': ismovible,
          'celda--bloqueada': !isjugador1 && !isjugador2 && isBloqueo
        };
      }
    },
    methods: {
      ControlClick() {
        this.BloquearCelda(this.rowIndex, this.celdaIndex);
        this.MovimientoJugador(this.rowIndex, this.celdaIndex);
        this.ControlClickCelda(this.rowIndex, this.celdaIndex);
      }
    }
  };
  </script>
<template>
    <div class = "celda" :class="celdaClass" @click="ControlClick"></div>
</template>
<style scoped>
  /* Bloque */
  .celda {
    width: 70px;
    height: 70px;
    border: 0.5px solid #72b0f7;
  }

  /* Modificador */
  .celda--inicio {
    background-color: lightblue;
  }

  .celda--ColorBase {
    background-color: #33659e;
  }

  .celda--jugador1 {
    background-color: red;
  }

  .celda--jugador2 {
    background-color: rgb(255, 162, 0);
  }

  .celda--movible {
    opacity: 0.6;
  }

  .celda--deshabilitado {
    pointer-events: none;
    opacity: 0.5;
  }

  .celda--bloqueada {
    background-color: #333333;
  }
</style>