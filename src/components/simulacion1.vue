<template>
    <div>
      <h1>Simulación de Operación de Aerolínea</h1>
      <div class="flights">
        <div v-for="flight in flights" :key="flight.id" class="flight">
          Vuelo {{ flight.id }} - Estado: {{ flight.status }}
        </div>
      </div>
      <button @click="addFlight">Agregar Vuelo</button>
      <button @click="removeFlight">Eliminar Vuelo</button>
      <button @click="startSimulation">Iniciar Simulación</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        flights: [],
        simulationInterval: null,
      };
    },
    methods: {
      addFlight() {
        const newFlight = {
          id: this.flights.length + 1,
          status: 'Pendiente',
        };
        this.flights.push(newFlight);
      },
      removeFlight() {
        this.flights.pop();
      },
      startSimulation() {
        if (this.flights.length === 0) {
          alert('No hay vuelos disponibles');
          return;
        }
        this.simulationInterval = setInterval(() => {
          const randomFlightIndex = Math.floor(Math.random() * this.flights.length);
          const flight = this.flights[randomFlightIndex];
          flight.status = 'En Progreso';
  
          setTimeout(() => {
            flight.status = 'Completado';
            if (this.flights.every((flight) => flight.status === 'Completado')) {
              clearInterval(this.simulationInterval);
            }
          }, Math.random() * 5000 + 2000);
        }, 1000);
      },
    },
  };
  </script>
  
  <style>
  .flights {
    display: flex;
    flex-wrap: wrap;
  }
  
  .flight {
    background-color: #ccc;
    border: 1px solid #999;
    border-radius: 5px;
    padding: 10px;
    margin-right: 5px;
    margin-bottom: 5px;
  }
  </style>
  
  