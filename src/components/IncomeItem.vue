<template>
  <div class="income-item">
    <div class="removeItem" @click="removeItem(income.id)">x</div>
    <div class="desc">{{ income.description }}</div>
    <div class="price">£ {{ income.value }}</div>
    <div class="date">{{ formattedDate }}</div>
  </div>
</template>

<script>
import { computed } from 'vue'

export default {
  props: {
    income: Object,
  },
  setup(props, { emit }) {

    const removeItem = incomeId => emit("removeItem", incomeId)

    const formattedDate = computed(() => {

      const currentDate = new Date(props.income.date)
      const day = currentDate.getDate()
      const month = currentDate.getMonth()
      const year = currentDate.getFullYear()

      return `${day}/${month}/${year}`
    })

    return { removeItem, formattedDate }
  },
}
</script>

<style scoped>
.income-item {
  position: relative;
  display: flex;
  padding: 15px 15px 15px 0px;
  background-color: #fff;
  border-radius: 8px;
  max-width: 600px;
  margin: 0 auto 30px;
}
.removeItem {
  color: #ef2d2d;
  font-weight: 600;
  font-size: 20px;
  line-height: 1;
  text-align: center;
  margin: 0 15px;
}
.desc {
  color: #666;
  flex: 1 1 100%;
  font-size: 20px;
}
.price {
  color: #666;
  min-width: 100px;
  font-size: 20px;
}
.date {
  color: #666;
  text-align: right;
  font-size: 20px;
}
</style>