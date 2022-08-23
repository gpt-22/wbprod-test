<template>
  <v-container fluid class="px-lg-20 py-9 px-7">
    <h1 class="mb-4 text-h5">Доставки</h1>

    <p class="mb-lg-8 mb-md-4 text--secondary text-subtitle-1 font-weight-regular subtitle">
      Как только выкуп оплачен, он моментально появится в доставках. Дальше мы отслеживаем его статус. "Доставлен" - можно забирать с пункта выдачи.
    </p>

    <v-row>
      <v-col v-for="order in orders" :key="order.id" xs="12" sm="6" md="4" lg="3" xl="2" class="mb-14">
        <order-card :order="order" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import OrderCard from "@/components/OrderCard"
import orders from "@/data/orders.json"

export default {
  name: "IndexPage",
  components: {
    OrderCard
  },
  data: function() {
    return {
      orders: []
    }
  },
  created() {
    // типа запрос на заказы
    this.orders = orders
  }
}
</script>

<style lang="scss" scoped>
.subtitle {
  line-height: 22px;
}
</style>