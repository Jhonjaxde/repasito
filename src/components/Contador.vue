<template>
  <div>
    <header>
      <h1>Juego POK&#201;MON</h1>
    </header>

    <section>
      <div class="container">
        <div class="juego">
          <div class="puntuacion">
            <p class="puntaje">Puntaje: {{ puntaje }}</p>
            <p class="intentos">Intentos: {{ intentos }}/3</p>
            <p>Selecciona el nombre de Pokémon correcto</p>
          </div>

          <div class="imagenPregunta">
            <img src="../img/image.png" v-show="mostrarImagenP" />
          </div>
          <div class="imagenRespuesta">
            <img src="../img/image2.png" v-show="mostrarImagenR" />
          </div>

          <div class="botones">
            <button
              v-for="(opcion, index) in opciones"
              :key="index"
              @click="verificarRespuesta(opcion)"
            >
              {{ opcion }}
            </button>

            <div class="botonR">
              <button @click="reiniciarJuego">Reiniciar</button>
            </div>

            <!-- Mensajes -->
            <p v-if="mostrarMensaje" class="mensaje">
              Felicitaciones, has seleccionado la opción correcta
            </p>
            <p v-if="mostrarMensajeMalo" class="mensajeMalo">
              Pokémon incorrecto, inténtalo nuevamente
            </p>
          </div>
        </div>
      </div>
    </section>

    <footer></footer>
  </div>
</template>
  
  <script>
export default {
  data() {
    return {
      opcionCorrecta: "drilbur",
      contador: 3,
      intentos: 1,
      puntaje: 5,
      mostrarMensaje: false,
      mostrarMensajeMalo: false,
      mostrarImagenP: true,
      mostrarImagenR: false,
      opciones: ["Keldeo-ordinary", "drilbur", "ninjask", "excadrill"],
    };
  },
  methods: {
    verificarRespuesta(opcionSeleccionada) {
      if (this.contador > 0) {
        if (opcionSeleccionada === this.opcionCorrecta) {
          this.mostrarMensaje = true;
          this.mostrarMensajeMalo = false;
          this.mostrarImagenP = false;
          this.mostrarImagenR = true;
        } else {
          this.contador--;
          this.intentos++;
          this.mostrarMensajeMalo = true;

          // Actualiza el puntaje basado en los intentos restantes
          this.puntaje = this.contador === 3 ? 5 : this.contador === 2 ? 3 : 1;

          // Si no quedan intentos
          if (this.contador === 0) {
            alert("Reinicie el juego");
            this.reiniciarJuego();
          }
        }
      }
    },
    reiniciarJuego() {
      this.contador = 3;
      this.intentos = 1;
      this.puntaje = 5;
      this.mostrarMensaje = false;
      this.mostrarMensajeMalo = false;
      this.mostrarImagenP = true;
      this.mostrarImagenR = false;
    },
  },
};
</script>
  
  <style scoped>
h1 {
  background-color: rgb(204, 230, 221);
  color: yellow;
  text-align: center;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.puntuacion {
  text-align: center;
  font-weight: bold;
  border: dashed;
  border-radius: 5px;
  border-color: blueviolet;
  padding: 10px 50px;
}

.imagenPregunta,
.imagenRespuesta {
  padding-left: 50px;
}



button {

  width: 200px;
  padding: 10px;
    margin-left: 100px;
  display: flex;
  align-items: center;
  gap: 5px;
}

button:hover {
  background-color: aquamarine;
}

.mensaje {
  background-color: blue;
  border: solid black;
  font-family: "Times New Roman", Times, serif;
  display: block;
  color: aliceblue;
}

.mensajeMalo {
  background-color: red;
  border: solid black;
  font-family: "Times New Roman", Times, serif;
  display: block;
}
</style>
  