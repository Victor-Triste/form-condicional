<template>
  <div class="py-5">
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
        :value="selectedOption"
        @change="updateSelectedOption"
      >
        <option disabled value="">Seleccione una opción</option>
        <option v-for="option in question.selectOptions" :key="option.value" :value="option.value">
          {{ option.label }}
        </option>
      </select>
    </form>

    <div v-if="selectedOption && inputPrompts.length > 0">
      <div v-for="(prompt, promptIndex) in inputPrompts" :key="promptIndex">
        <label
          :for="'input-' + index + '-' + promptIndex"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >
          {{ prompt.label }}
        </label>
        <input
          v-if="prompt.type === 'text'"
          :type="prompt.type"
          :id="'input-' + index + '-' + promptIndex"
          :placeholder="prompt.placeholder"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        />
        <textarea
          v-else-if="prompt.type === 'textarea'"
          :id="'input-' + index + '-' + promptIndex"
          :placeholder="prompt.placeholder"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        ></textarea>
        <!-- Añade más tipos de input según sea necesario -->
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  index: Number,
  question: Object,
  selectedOption: String,
});

const emit = defineEmits(['update:selectedOption']);

const updateSelectedOption = (event) => {
  emit('update:selectedOption', event.target.value);
};

const inputPrompts = computed(() => {
  const selected = props.question.selectOptions.find(
    (option) => option.value === props.selectedOption,
  );
  return selected ? selected.inputPrompts : [];
});
</script>
<!-- <template>
  <div class="py-5">
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
        :value="selectedOption"
        @change="updateSelectedOption"
      >
        <option disabled value="">Seleccione una opción</option>
        <option v-for="option in question.selectOptions" :key="option.value" :value="option.value">
          {{ option.label }}
        </option>
      </select>
    </form>

    
    <div v-if="selectedOption && getInputPrompt" class="pt-3">
      <label
        :for="'input-' + index"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
      >
        {{ getInputPrompt }}
      </label>
      <input
        type="text"
        :id="'input-' + index"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
      />
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  index: Number,
  question: Object,
  selectedOption: String,
});

const emit = defineEmits(['update:selectedOption']);

const updateSelectedOption = (event) => {
  emit('update:selectedOption', event.target.value);
};

// const getInputPrompt = computed(() => {
//   const selected = props.question.selectOptions.find(
//     (option) => option.value === props.selectedOption,
//   );
//   return selected ? selected.inputPrompt : null;
// });

const getInputPrompts = computed(() => {
  const selected = props.question.selectOptions.find(
    (option) => option.value === props.selectedOption,
  );
  return selected && selected.inputPrompts ? selected.inputPrompts : [];
});
</script> -->
