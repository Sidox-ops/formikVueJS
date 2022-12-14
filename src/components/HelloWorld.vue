<script setup>
import Formik from "../components/Formik.vue";
import Field from "../components/Field.vue";
import { reactive, ref } from "vue";

const _initialValues = reactive({
  name: "sidox",
  email: "",
  color: "red",
  isDeveloper: true,
});

function validate(values) {
  console.log("Validate trigger >>>", values);
}

function onSubmit(values) {
  console.log("On submit trigger >>>", values);
}

</script>

<template>
  <Formik
    :initialValues="_initialValues"
    :validate="validate"
    :onSubmit="onSubmit"
  >
    <template #default="{ values, errors, handleChange, handleSubmit }">
      <form @submit.prevent="handleSubmit">
        <p>
          <!-- handle change on Field -->
          
          <Field
          
          v-model:value="values.name"
          type="text" name="name" as="input" placeholder="Enter name" />
          <!-- <span v-if="errors.name">{{ errors.name }}</span> -->
        </p>
        <p>
          <Field
          v-model:value="values.email"
            type="email"
            name="email"
            as="input"
            placeholder="Enter email"
          />
          <!-- <span v-if="errors.email">{{ errors.email }}</span> -->
        </p>
        <p>
          Are you a developer ?
          <Field v-model:value="values.isDeveloper"
           type="checkbox" name="isDeveloper" as="input" />
          <br>
          <Field 
            v-model:value="values.color"
          name="color" as="select">
            <template #default>
              <option value="red">Red</option>
              <option value="green">Green</option>
              <option value="blue">Blue</option>
            </template>
          </Field>
        </p>
        <button type="submit">Submit</button>
      </form>
    </template>
  </Formik>
</template>

<style scoped></style>