<script setup>
import { provide, reactive, ref, inject } from "vue";
import { valuesKey } from "./providers/FormikProviderKeys.js";

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
const formData = inject(valuesKey);
// console.log("Field formData", formData);

// const value = ref("");

function handleChange(event) {
  console.log("Handle change trigger", event.target.value, formData);
  formData.values[props.name] = event.target.value;
}

</script>

<template>
  <component :is="as" :type="type" :name="name" :value="value"
  @input="handleChange"
    ><slot></slot
  ></component>
</template>

<style scoped></style>
