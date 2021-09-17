<template>
  <div class="formulario">
    <div class="formulario-titulo">
      <h1>Random GIF Cat</h1>
    </div> 
    <form @submit.prevent="generarNuevoGatitoUrl()"> 
      <div class="formulario-inputs">
      <label for="titulo">Titulo:</label>
      <input
        type="text"
        required
        name="titulo"
        minlength="3"
        maxlength="10"
        v-model="formulario.titulo"
      />
      <label for="filtro">Filtro:</label>
      <select required name="filtro" v-model="formulario.filtro">
        <option value="" selected disabled></option>
        <option value="blur">Blur</option>
        <option value="mono">Mono</option>
        <option value="sepia">Sepia</option>
        <option value="negative">Negative</option>
        <option value="paint">Paint</option>
      </select>
      <label for="color">Color:</label>
      <select required name="color" v-model="formulario.color">
        <option value="" selected disabled></option>
        <option value="red">Rojo</option>
        <option value="blue">Azul</option>
        <option value="green">Verde</option>
        <option value="purple">Morado</option>
        <option value="orange">Naranja</option>
      </select>
      <div
        style="width: 15px; height: 15px; border-radius: 50%; display: inline-block"
        :style="{ 'background-color': formulario.color }"
      ></div>
      <label for="tamaño">Tamaño:</label>
      <input
        type="number"
        name="tamaño"
        required
        step="100"
        min="100"
        max="900"
        v-model.number="formulario.tamaño"
      />
      <div class="formulario-boton">
        <button type="submit">Obtener mi gatito</button>
      </div>
      </div>
    </form>
    <img
      alt="gatito"
      :src="gatitoUrl"
      @load="cargandoGatito = false"
      v-show="gatitoUrl !== '' && !cargandoGatito"
    />
    {{ cargandoGatito ? "Cargando imagen del gatito" : "" }}

  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    cargandoGatito: false,
    cargandoGatitoConBlob: false,
    gatitoUrl: "",
    gatitoUrlConBlob: "",
    formulario: {
      titulo: null,
      filtro: null,
      color: null,
      tamaño: null,
    },
  }),
  methods: {
    generarNuevoGatitoUrl() {
      this.cargandoGatito = true;

      this.gatitoUrl = `https://cataas.com/cat/gif/says/${this.formulario.titulo}?filter=${this.formulario.filtro}&color=${this.formulario.color}&width=${this.formulario.tamaño}&height=${this.formulario.tamaño}`;
    },
  },
};
</script>

<style>
body{
  margin:0px;
  display: grid;
}
.formulario{
  text-align:center;
  background-color: #d292bb;
}
.formulario-titulo{ 
  padding: 30px;
  color: #fff;
  background-color: #00d0ff;
}
.formulario-inputs{
 padding-top: 30px;
}
.formulario-inputs label{
  display: inline;
  display: grid;
  padding: 5px;
}
.formulario-boton{
  padding: 20px;
}
</style>
