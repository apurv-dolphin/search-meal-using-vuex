<template>
  <div class="max-w-[800px] mx-auto p-8">
    <h1 class="text-4xl font-bold mb-5 text-[#2c6ef7]">{{ meal.strMeal }}</h1>
    <div class="flex justify-center m-2">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="w-full max-w-[45%] sm:max-w-[30%]"
      />
    </div>
    <div class="p-4">
      <h1 class="text-2xl font-bold mb-4">Dark Mode Toggle data</h1>

      <!-- Dark Mode Toggle Switch -->
      <div class="relative inline-block w-10 align-middle">
        <input
          type="checkbox"
          id="darkModeToggle"
          class="dark:bg-gray-600 dark:checked:bg-[#2c6ef7] cursor-pointer"
          v-model="isDarkMode"
        />
        <div :class="{ 'text-red-500': isDarkMode }">Apurv</div>
      </div>
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>
      <div><strong class="font-bold">Area:</strong> {{ meal.strArea }}</div>
      <div><strong class="font-bold">Tags:</strong> {{ meal.strTags }}</div>
    </div>

    <div class="my-3">
      {{ meal.strInstructions }}
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-2">Ingredients</h2>
        <ul>
          <template v-for="(el, index) of new Array(20)">
            <li v-if="meal[`strIngredient${index + 1}`]" :key="index">
              {{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-2">Measures</h2>
        <ul>
          <template v-for="(el, index) of new Array(20)">
            <li v-if="meal[`strMeasure${index + 1}`]" :key="index">
              {{ index + 1 }}. {{ meal[`strMeasure${index + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div class="mt-4">
        <YouTubeButton :href="meal.strYoutube" />
        <a
          :href="meal.strSource"
          target="_blank"
          class="ml-3 px-3 py-2 rounded border-2 border-transparent text-indigo-600 transition-colors"
        >
          View Original Source
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, watchEffect } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YouTubeButton from "../components/YouTubeButton.vue";

const route = useRoute();
const meal = ref({});
const isDarkMode = ref(false);

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
  });
});

watchEffect(() => {
  document.body.classList.toggle("dark", isDarkMode.value);
});
</script>
