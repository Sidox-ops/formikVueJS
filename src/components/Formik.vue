<script setup>
import { reactive, provide } from "vue";
import {
  values as valuesKey,
  setValueChange as setValueChangeKey,
} from "./providers/FormikProviderKeys.js";

const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  validate: {
    type: Function,
    required: false,
  },
  onSubmit: {
    type: Function,
    required: true,
  },
});

const values = reactive(props.initialValues);

function handleSubmit() {
  console.log("Handle submit trigger", values);
}

function handleChange(event) {
  console.log("Handle change trigger", event.target.value);
  value.value = event.target.value;
  setValueChange(props.name, event.target.value);
}

function setValueChange(name, value) {
  console.log("Set value change trigger", name, value);
  values[name] = value;
}

provide(valuesKey, setValueChange);
</script>

<template>
  <div>
    <slot
      :values="values"
      :errors="errors"
      :handleChange="handleChange"
      :handleSubmit="handleSubmit"
    ></slot>
  </div>
</template>

<style scoped></style>