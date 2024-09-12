<template>
  <div class="image-carousel">
    <h3>Image Carousel</h3>
    <div class="carousel">
      <div
        class="carousel-images"
        :style="{
          transform: `translateX(-${currentIndex * 100}%)`,
          transition: isTransitioning ? 'transform 0.5s ease' : 'none',
        }"
        @transitionend="handleTransitionEnd"
      >
        <img
          v-for="(image, index) in displayedImages"
          :key="index"
          :src="image"
          alt="Carousel Image"
          class="carousel-image"
        />
      </div>
    </div>
    <div class="controls">
      <button @click="prevImage" class="carousel-button">Previous</button>
      <button @click="nextImage" class="carousel-button">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      currentIndex: 1, // Mulai dari index 1 karena kita memiliki gambar kloning pertama dan terakhir
      isTransitioning: true, // Kontrol apakah transisi animasi diaktifkan
    };
  },
  computed: {
    // Menambahkan gambar kloning di awal dan akhir untuk infinite loop
    displayedImages() {
      return [
        this.images[this.images.length - 1], // Kloning gambar terakhir di awal
        ...this.images, // Gambar asli
        this.images[0], // Kloning gambar pertama di akhir
      ];
    },
  },
  mounted() {
    this.generateRandomImages();
  },
  methods: {
    generateRandomImages() {
      // Menghasilkan 5 gambar acak dari layanan placeholder
      for (let i = 1; i <= 5; i++) {
        const randomImage = `https://picsum.photos/600/300?random=${Math.floor(
          Math.random() * 1000
        )}`;
        this.images.push(randomImage);
      }
    },
    nextImage() {
      if (this.currentIndex < this.images.length) {
        this.currentIndex++;
      } else {
        // Ketika mencapai gambar kloning terakhir, lompat ke gambar pertama tanpa transisi
        this.currentIndex++; // Naik ke kloning pertama
      }
    },
    prevImage() {
      if (this.currentIndex > 0) {
        this.currentIndex--;
      } else {
        // Ketika mencapai gambar kloning pertama, lompat ke gambar terakhir tanpa transisi
        this.currentIndex--; // Turun ke kloning terakhir
      }
    },
    handleTransitionEnd() {
      // Reset currentIndex ketika mencapai gambar kloning untuk infinite loop
      if (this.currentIndex === this.images.length + 1) {
        this.isTransitioning = false; // Matikan transisi untuk lompat tanpa animasi
        this.currentIndex = 1; // Lompat ke gambar pertama asli
      }
      if (this.currentIndex === 0) {
        this.isTransitioning = false; // Matikan transisi untuk lompat tanpa animasi
        this.currentIndex = this.images.length; // Lompat ke gambar terakhir asli
      }
      setTimeout(() => {
        this.isTransitioning = true; // Aktifkan kembali transisi setelah reset
      }, 50); // Sedikit jeda sebelum mengaktifkan kembali transisi
    },
  },
};
</script>

<style scoped>
.image-carousel {
  text-align: center;
  margin: 40px auto;
  padding: 20px;
  max-width: 600px;
  background-color: #f9fafc;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  position: relative;
}

h3 {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 20px;
}

.carousel {
  overflow: hidden;
  width: 100%;
  position: relative;
}

.carousel-images {
  display: flex;
  transition: transform 0.5s ease;
}

.carousel-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
  user-select: none;
}

.controls {
  margin-top: 20px;
}

.carousel-button {
  padding: 12px 25px;
  background-color: #e74c3c;
  color: white;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
  margin: 0 10px;
}

.carousel-button:hover {
  background-color: #c0392b;
  transform: scale(1.05);
}

/* Responsiveness for smaller screens */
@media (max-width: 768px) {
  .image-carousel {
    max-width: 100%;
    padding: 10px;
  }
  .carousel-button {
    padding: 10px 20px;
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .carousel-button {
    padding: 8px 15px;
    font-size: 0.8rem;
  }
}
</style>
