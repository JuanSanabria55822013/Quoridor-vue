
  <script>
  export default {
    props: {
      ganador: Number
    },
    data() {
      return {
        MostrarModal: true
      };
    },
    methods: {
      resetGame() {
        this.$emit('reset');
      }
    }
  }
  </script>

  <template>
    <div class="modal" v-if="MostrarModal">
      <div class="modal-content">
        <p>¡Ganaste jugador {{ ganador }}!</p>
        <button class="modal-content__reset-button" @click="resetGame">Reiniciar</button>
      </div>
    </div>
  </template>
  
  <style scoped>

/* Bloque */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #1a1a1d;
  padding: 20px;
  border: 2px solid #c3073f;
  border-radius: 10px;
  width: 80%;
  max-width: 600px;
  max-height: 300px;
  text-align: center;
  text-justify: center;
  color: white;
  font-family: 'Arial', sans-serif;
  animation: fadeIn 0.5s;
}

/* Elemento */
.modal-content__reset-button {
  background-color: #c3073f;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

/* Modificador */
.modal-content__reset-button--hover {
  background-color: #ff6f61;
}

/* Animation */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
  </style>