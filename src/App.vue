<template>
  <div class="flex flex-col items-center justify-center min-h-screen">
    <QuestionForm
      v-for="(question, index) in questions"
      :key="index"
      :question="question"
      v-model:selectedOption="selectedOptions[index]"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import QuestionForm from './components/QuestionForm.vue';

const questions = ref([]);
const selectedOptions = ref([]);

// Cargar las preguntas desde el JSON
const loadQuestions = async () => {
  try {
    const response = await fetch('/questions.json');
    questions.value = await response.json();
    initializeSelectedOptions();
  } catch (error) {
    console.error('Error loading questions:', error);
  }
};

// Inicializar selectedOptions con valores vacíos
const initializeSelectedOptions = () => {
  selectedOptions.value = questions.value.map(() => '');
};

// Cargar las preguntas cuando el componente se monta
onMounted(() => {
  loadQuestions();
});
</script>

<!-- <template>
  <div class="flex flex-col items-center justify-center min-h-screen">
    <div v-for="(question, index) in questions" :key="index" class="w-1/2 mb-6">
      <form>
        <label
          :for="'select-' + index"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >
          {{ question.question }}
        </label>
        <select
          :id="'select-' + index"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          v-model="selectedOptions[index]"
        >
          <option disabled value="">Seleccione una opción</option>
          <option
            v-for="option in question.selectOptions"
            :key="option.value"
            :value="option.value"
          >
            {{ option.label }}
          </option>
        </select>
      </form>

      <div v-if="selectedOptions[index] && getInputPrompt(index)">
        <label
          :for="'input-' + index"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >
          {{ getInputPrompt(index) }}
        </label>
        <input
          type="text"
          :id="'input-' + index"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const questions = ref([]);
const selectedOptions = ref([]);

// Inicializar selectedOptions con valores vacíos
onMounted(() => {
  loadQuestions();
  initializeSelectedOptions();
});

const loadQuestions = async () => {
  try {
    const response = await fetch('/questions.json');
    questions.value = await response.json();
    initializeSelectedOptions();
  } catch (error) {
    console.error('Error loading questions:', error);
  }
};

const initializeSelectedOptions = () => {
  selectedOptions.value = questions.value.map(() => '');
};

const getInputPrompt = (index) => {
  const selectedOption = questions.value[index].selectOptions.find(
    (option) => option.value === selectedOptions.value[index],
  );
  return selectedOption ? selectedOption.inputPrompt : null;
};
</script> -->
