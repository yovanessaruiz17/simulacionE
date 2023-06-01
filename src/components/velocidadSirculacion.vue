<template>
    <div>
      <h1>Simulación de Velocidad de Circulación</h1>
      <div class="input-container">
        <label for="distance">Distancia recorrida (metros):</label>
        <input type="number" id="distance" v-model="distance">
      </div>
      <div class="input-container">
        <label for="time">Tiempo transcurrido (minutos):</label>
        <input type="number" id="time" v-model="time">
      </div>
      <button @click="calculateSpeed">Calcular Velocidad</button>
      <div v-if="speedCalculated" class="result">
        La velocidad de circulación es de {{ speed.toFixed(2) }} metros por segundo.
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        distance: null,
        time: null,
        speed: null,
        speedCalculated: false,
      };
    },
    methods: {
      calculateSpeed() {
        if (this.distance === null || this.time === null) {
          alert('Por favor, ingresa todos los datos necesarios.');
          return;
        }
        const distanceInMeters = this.distance;
        const timeInMinutes = this.time;
        const timeInSeconds = timeInMinutes * 60;
        this.speed = distanceInMeters / timeInSeconds;
        this.speedCalculated = true;
      },
    },
  };
  </script>
  
  <style>
  .input-container {
    margin-bottom: 10px;
  }
  
  .result {
    margin-top: 20px;
  }
  </style>
  