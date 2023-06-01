<template>
    <div>
      <h1>Simulación de Embarque de Pasajeros</h1>
      <div class="input-container">
        <label for="passengerCount">Cantidad de pasajeros:</label>
        <input type="number" id="passengerCount" v-model="passengerCount">
      </div>
      <div class="input-container">
        <label for="boardingTime">Tiempo de embarque por pasajero (segundos):</label>
        <input type="number" id="boardingTime" v-model="boardingTime">
      </div>
      <div class="input-container">
        <label for="planeCapacity">Capacidad del avión:</label>
        <input type="number" id="planeCapacity" v-model="planeCapacity">
      </div>
      <button @click="startBoarding">Iniciar Embarque</button>
      <div v-if="boardingInProgress" class="progress-bar">
        <div class="progress" :style="{ width: progressWidth }"></div>
      </div>
      <div v-if="boardingComplete" class="result">
        ¡El embarque de pasajeros ha finalizado!
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
    computed: {
      progressWidth() {
        if (this.passengerCount === null || this.planeCapacity === null) {
          return '0%';
        }
        const percentage = (this.passengersBoarded / this.passengerCount) * 100;
        return `${percentage}%`;
      },
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
  
  .progress-bar {
    width: 100%;
    height: 20px;
    background-color: #eee;
    margin-top: 20px;
  }
  
  .progress {
    height: 100%;
    background-color: #2196f3;
    transition: width 0.5s;
  }
  
  .result {
    margin-top: 20px;
  }
  </style>
  