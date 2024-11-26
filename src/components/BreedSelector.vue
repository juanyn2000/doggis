<template>
  <div class="select-container">
    <select @change="breedSelected" class="custom-select">
      <option value="" selected disabled>Seleccione una raza</option>
      <option v-for="breed in breeds" :key="breed" :value="breed">{{ breed }}</option>
    </select>
  </div>
  
</template>

<script>
export default {
  name: "BreedSelector",
  data() {
    return {
      breeds: [],
    };
  },
  methods: {
    async getBreeds() {
      try {
        const response = await fetch("https://dog.ceo/api/breeds/list/all");
        const data = await response.json();
        this.breeds = Object.keys(data.message);
        console.log(this.breeds);
      } catch (error) {
        console.error(error);
      }
    },
    breedSelected(event){
        const selectedBreed = event.target.value;
        this.$emit('breed-selected', selectedBreed);
    }
  },
  mounted() {
    this.getBreeds();
  },
};
</script>

<style scoped>
/* Contenedor para centrar el select */
.select-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px 0;
}

/* Estilo para el elemento select */
.custom-select {
  width: 300px;
  padding: 10px 15px;
  font-size: 1rem;
  font-family: Arial, sans-serif;
  border: 2px solid #4caf50;
  border-radius: 8px;
  background-color: #f9f9f9;
  color: #333;
  outline: none;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  appearance: none; /* Para ocultar el estilo nativo en navegadores */
}

/* Efecto al pasar el mouse */
.custom-select:hover {
  border-color: #3b9e3b;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* Estilo al hacer foco */
.custom-select:focus {
  border-color: #2e7d32;
  box-shadow: 0 0 5px rgba(46, 125, 50, 0.5);
}

/* Opciones */
.custom-select option {
  padding: 10px;
  background-color: #fff;
  color: #333;
}

/* Deshabilitar primera opción */
.custom-select option:disabled {
  color: #aaa;
  font-style: italic;
}

</style>
