<template>
    <div>
      <h1>Simulación de Consumo de Combustible</h1>
      <div class="input-container">
        <label for="distance">Distancia del vuelo (km):</label>
        <input type="number" id="distance" v-model="distance">
      </div>
      <div class="input-container">
        <label for="efficiency">Eficiencia del motor (l/km):</label>
        <input type="number" id="efficiency" v-model="efficiency">
      </div>
      <button @click="calculateFuelConsumption">Calcular Consumo</button>
      <div v-if="fuelConsumption !== null" class="result">
        El avión consumió {{ fuelConsumption }} litros de combustible en el vuelo de {{ distance }} km.
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        distance: null,
        efficiency: null,
        fuelConsumption: null,
      };
    },
    methods: {
      calculateFuelConsumption() {
        if (this.distance === null || this.efficiency === null) {
          alert('Por favor, ingresa la distancia y la eficiencia del motor.');
          return;
        }
        this.fuelConsumption = this.distance * this.efficiency;
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
  