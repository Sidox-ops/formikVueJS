<script setup>
import { provide, reactive, ref, inject } from "vue";
import { setValueChange as setValueChangeKey } from "./providers/FormikProviderKeys.js";

defineProps({
  name: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    required: false,
    default: "text",
  },
  as: {
    type: String,
    required: false,
  },
  OnChange: {
    type: Function,
    required: false,
  },
});

// inject values from Formik
const setValueChange = inject(setValueChangeKey);

// const value = ref("");

function handleChange(event) {
  console.log("Handle change trigger", event.target.value);
  value.value = event.target.value;
  setValueChange(props.name, event.target.value);
}

// provide(setValueChangeKey, setValueChange);
</script>

<template>
  <component :is="as" :type="type" :name="name" :value="value"
    ><slot></slot
  ></component>
</template>

<style scoped></style>
