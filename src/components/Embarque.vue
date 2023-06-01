<template>
    <div>
      <h1>Simulación de Embarque de Pasajeros</h1>
      <div class="input-container">
        <label for="passengerCount">Cantidad de pasajeros:</label>
        <input type="number" id="passengerCount" v-model="passengerCount">
      </div>
      <div class="input-container">
        <label for="boardingTime">Tiempo de embarque por pasajero (minutos):</label>
        <input type="number" id="boardingTime" v-model="boardingTime">
      </div>
      <div class="input-container">
        <label for="planeCapacity">Capacidad del avión:</label>
        <input type="number" id="planeCapacity" v-model="planeCapacity">
      </div>
      <button @click="startBoarding">Iniciar Embarque</button>
      <div v-if="boardingInProgress" class="boarding-status">
        Pasajeros embarcados: {{ passengersBoarded }} / {{ passengerCount }}
      </div>
      <div v-if="boardingComplete" class="result">
        ¡El embarque de pasajeros ha finalizado!
      </div>
      <div v-if="boardingInProgress" class="result">
        Tiempo total de embarque: {{ totalBoardingTime }} minutos
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        passengerCount: null,
        boardingTime: null,
        planeCapacity: null,
        boardingInProgress: false,
        passengersBoarded: 0,
        boardingComplete: false,
      };
    },
    methods: {
      startBoarding() {
        if (this.passengerCount === null || this.boardingTime === null || this.planeCapacity === null) {
          alert('Por favor, ingresa todos los datos necesarios.');
          return;
        }
        this.boardingInProgress = true;
        this.boardPassengers();
      },
      boardPassengers() {
        const boardingInterval = setInterval(() => {
          this.passengersBoarded++;
          this.totalBoardingTime = this.passengerCount * this.boardingTime;
          if (this.passengersBoarded >= this.passengerCount) {
            clearInterval(boardingInterval);
            this.boardingInProgress = false;
            this.boardingComplete = true;
          }
        }, this.boardingTime * 1000);
      },
    },
  };
  </script>
  
  <style>
  .input-container {
    margin-bottom: 10px;
  }
  
  .boarding-status {
    margin-top: 20px;
  }
  
  .result {
    margin-top: 20px;
  }
  </style>
  