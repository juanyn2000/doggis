<template>
  <div class="galeria">
    <div class="cont-card" v-for="image in images" :key="image">
      <img :src="image" class="img-fixed" alt="dog" />
    </div>
  </div>
</template>

<script>
export default {
  name: "DogGallery",
  props: {
    breed: "",
  },
  data() {
    return {
      images: [],
    };
  },
  methods: {
    async getImages(currentbreed) {
      try {
        const response = await fetch(
          `https://dog.ceo/api/breed/${currentbreed}/images`
        );
        const data = await response.json();
        this.images = data.message;
        console.log(this.images);
      } catch (error) {
        console.error(error);
      }
    },
  },
  watch: {
    breed(newBreed) {
      this.getImages(newBreed);
    },
  },
};
</script>

<style scoped>
.galeria {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
  padding: 1rem;
}
.cont-card {
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 10px;
}
.img-fixed {
  width: 200px;
  height: 200px;
  border-radius: 5px;
}
</style>
