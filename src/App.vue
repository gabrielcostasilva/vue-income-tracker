<template>
  <Header :totalIncome="state.totalIncome" />
  <Form @add-income="addIncome" />
  <IncomeList :state="state" />
</template>

<script>
import Header from '@/components/Header'
import Form from '@/components/Form'
import IncomeList from '@/components/IncomeList'

import { computed, reactive } from 'vue'

export default {
  components: { Header, Form, IncomeList },
  setup() {
    const state = reactive({
      income: [],
      totalIncome: computed(() =>
        state.income.reduce(
          (acumulator, currentIncome) => (acumulator += currentIncome.value),
          0
        )
      ),
      sortedIncome: computed(() =>
        state.income.sort((a, b) => b.date - a.date)
      ),
    })

    const addIncome = (data) => {
      let splittedDate = data.date.split('-')
      let formattedDate = new Date(
        splittedDate[0],
        splittedDate[1],
        splittedDate[2]
      )

      state.income.push({
        id: Math.floor(Math.random() * 100000),
        description: data.description,
        value: parseInt(data.value),
        date: formattedDate.getTime(),
      })
    }

    return {
      state,
      addIncome,
    }
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}
body {
  background: #eee;
}
</style>
