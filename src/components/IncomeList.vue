<template>
  <div class="income-list">
    <IncomeItem @removeItem="removeItem" v-for="data in state.sortedIncome" :key="data.id" :income="data" />
  </div>
</template>

<script>
import IncomeItem from './IncomeItem'

export default {
  components: { IncomeItem },
  props: {
    state: Object,
  },
  setup(props, {emit}) {
    
    const removeItem = id => emit("removeItem", id)

    return { removeItem }
  }
}
</script>

<style scoped>
.income-list {
  margin-top: 30px;
  padding: 15px;
}
</style>