<template>
  <div
    v-if="showPopup"
    class="fixed inset-0 flex justify-center items-center bg-gray-900 bg-opacity-75 z-50"
  ></div>
  <!-- Advertisement Popup -->
  <div
    class="fixed inset-0 flex justify-center items-center z-50"
    v-if="showPopup"
  >
    <div class="bg-white rounded-lg p-8 max-w-md">
      <h2 class="text-2xl font-semibold mb-4">Discover New Recipes!</h2>
      <p class="text-gray-700 mb-6">
        Check out our latest collection of mouthwatering recipes for foodies.
      </p>
      <button
        class="bg-yellow-500 hover:bg-yellow-600 text-white font-semibold py-2 px-4 rounded-md"
      >
        Explore Now
      </button>
      <button
        class="mt-2 ml-3 bg-red-600 hover:bg-[#f43f5e] text-white text-sm font-semibold py-2 px-4 rounded-md"
        @click="closePopup"
      >
        Close
      </button>
    </div>
  </div>
  <router-view />
</template>

<script>
export default {
  data() {
    return {
      showPopup: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showPopup = true; // Show the popup after 10 second
    }, 10000);
  },
  methods: {
    closePopup() {
      this.showPopup = false;
    },
  },
};
</script>
<style scoped>
/* CSS Styling */
.fixed {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

/* Center the content vertically and horizontally */
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Set the background color and opacity */
.bg-gray-900 {
  background-color: #1a202c;
}

.bg-opacity-75 {
  opacity: 0.75;
}

/* Style the popup container */
.bg-white {
  background-color: #fff;
}

/* Add padding and round the corners of the popup */
.rounded-lg {
  border-radius: 0.5rem;
}

.p-8 {
  padding: 2rem;
}

/* Style the title and description text */
.text-2xl {
  font-size: 1.5rem;
  line-height: 2rem;
}

.text-gray-700 {
  color: #4a5568;
}

/* Style the buttons */
.text-white {
  color: #fff;
}

.bg-yellow-500 {
  background-color: #fbbf24;
}

.hover\:bg-yellow-600:hover {
  background-color: #d97706;
}

.text-sm {
  font-size: 0.875rem;
}

.text-gray-600 {
  color: #718096;
}

.hover\:text-gray-800:hover {
  color: #2d3748;
}

/* Add margin to the close button */
.mt-2 {
  margin-top: 0.5rem;
}

/* Add underline on hover for close button */
.underline:hover {
  text-decoration: underline;
}

/* Add cursor pointer on hover for close button */
.cursor-pointer {
  cursor: pointer;
}

/* Set z-index for popup overlay */
.z-50 {
  z-index: 50;
}
</style>
