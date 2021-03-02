<template>
  <form @submit.prevent="formHandler">
    <input
      type="text"
      v-model="formData.description"
      placeholder="Description ..."
    />
    <input type="number" v-model="formData.value" placeholder="Value ..." />
    <input type="date" v-model="formData.date" placeholder="Date ..." />
    <input type="submit" value="SUBMIT" />
  </form>
</template>

<script>
import { reactive } from 'vue'
export default {
  props: {
    state: Object,
  },
  setup(props, { emit }) {
    const formData = reactive({
      description: null,
      value: null,
      date: null,
    })

    const formHandler = () => {
      emit('add-income', {
        description: formData.description,
        value: formData.value,
        date: formData.date,
      })

      formData.description = null
      formData.value = null
      formData.date = null
    }

    return {
      formData,
      formHandler,
    }
  },
}
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}
form input {
  color: #888;
  border: none;
  outline: none;
  font-size: 20px;
}
form input::placeholder {
  color: #aaa;
}
form input:not([type='submit']) {
  display: block;
  background: #fff;
  border: none;
  outline: none;
  padding: 5px 15px;
}
form input[type='submit'] {
  display: block;
  background: none;
  border: none;
  outline: none;
  color: #fff;
  font-weight: 500;
  text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  padding: 5px 15px;
  background-color: #ffce00;
  cursor: pointer;
}
form input:first-of-type {
  border-radius: 8px 0px 0px 8px;
}
form input:last-of-type {
  border-radius: 0px 8px 8px 0px;
}
</style>