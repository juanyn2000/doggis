<script>
import BreedSelector from "@/components/BreedSelector.vue";
import DogGallery from "@/components/DogGallery.vue";

export default {
  components: {
    BreedSelector,
    DogGallery,
  },
  data() {
    return {
      selectedBreed: "",
    };
  },
  methods: {
    updateBreed(breed) {
      this.selectedBreed = breed;
    },
  },
};
</script>

<template>
  <h1 class="arc-title">
    <span class="span1">FOTITOS</span> DE  <span class="span2"> PERRITOS</span>
  </h1>
  
  <main>
    <BreedSelector @breed-selected="updateBreed" />
    <div>
      <DogGallery :breed="selectedBreed" />
    </div>
  </main>
</template>

<style scoped>

.arc-title span {
  display: inline-block;
  transform-origin: bottom center;
}

.span1 {
  transform: rotate(-20deg); /* Rotación para el lado izquierdo */
}

.span2 {
  transform: rotate(20deg); /* Rotación para el lado derecho */
}



h1 {
  font-size: 2rem; /* Ajusta según el tamaño deseado */
  font-family: Arial, sans-serif;
  color: white;
  margin-bottom: 20px;
  text-align: center;
}

</style>
