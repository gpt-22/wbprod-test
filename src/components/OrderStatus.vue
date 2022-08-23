<template>
  <v-chip label :color="color" class="px-2 py-1 status">
    {{ text }}
  </v-chip>
</template>

<script>
// Типа мапа статусов
const ORDER_STATUSES = {
  created: {
    text: "Создан",
    color: "#039BE5"
  },
  inProcess: {
    text: "В процессе сборки",
    color: "#29B6F6"
  },
  inWayToPickupPoint: {
    text: "В пути на пункт выдачи",
    color: "#F7981C"
  },
  delivered: {
    text: "В пункте выдачи",
    color: "#43A047"
  },
  canceled: {
    text: "Отменен",
    color: "#EF6C00"
  },
}

export default {
  name: "OrderStatus",
  props: {
    status: {
      type: String,
      required: true
    }
  },
  computed: {
    text() {
      return ORDER_STATUSES[this.status].text.toUpperCase()
    },
    color() {
      return ORDER_STATUSES[this.status].color
    }
  }
}
</script>

<style lang="scss" scoped>
.status {
  font-size: 12px;
  line-height: 14px;
}
</style>