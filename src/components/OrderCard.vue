<template>
  <v-card class="pa-4 fill-height rounded-md">
    <div class="d-flex flex-column fill-height card-content">
      <div class="d-flex justify-space-between align-start">
        <div class="d-flex flex-column">
          <span class="grey--text text-body-2">Заказ:</span>
          <span class="text-body-1 text-break">{{ order.id }}</span>
        </div>
        <v-icon class="ml-1" color="secondary">
          mdi-upload
        </v-icon>
      </div>

      <div class="d-flex">
        <img :src="imageUrl" alt="no-order-image" class="mr-3 order-image">
        <div class="d-flex flex-column fill-height justify-space-between">
          <h3 class="text-body-1 order-title mb-1">{{ order.title}}</h3>
          <div class="order-vendor-code">Aрт. {{ order.vendorСode}}</div>
        </div>
      </div>

      <div>
        <order-status :status="order.status" />
      </div>

      <div v-if="order.datetime?.length" class="d-flex">
        <div class="mr-8">
          <v-icon class="mr-1">mdi-calendar-range</v-icon>
          <span class="text-body-1">{{ orderDate }}</span>
        </div>
        <div>
          <v-icon class="mr-1">mdi-clock</v-icon>
          <span class="text-body-1">{{ orderTime }}</span>
        </div>
      </div>

      <div v-if="order.receiver" class="d-flex flex-column">
        <span class="grey--text">Получатель:</span>
        <span class="text-body-1">{{ receiverText }}</span>
      </div>

      <div v-if="order.address?.length" class="d-flex flex-column">
        <span class="grey--text">Адрес:</span>
        <span class="text-body-1">{{ order.address }}</span>
      </div>

      <div class="mt-auto">
        <v-btn block outlined color="primary ">
          ПОЛУЧЕНИЕ ПО QR-КОДУ
        </v-btn>
      </div>
    </div>
  </v-card>
</template>

<script>
import OrderStatus from "@/components/OrderStatus"

export default {
  name: "OrderCard",
  props: {
    order: {
      type: Object,
      required: true
    }
  },
  components: {
    OrderStatus
  },
  computed: {
    imageUrl() {
      return require(`@/assets/images/${this.order.image}`)
    },
    orderDate() {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      const date = new Date(this.order.datetime)
      const formattedDate =  new Intl.DateTimeFormat('ru-RU', options).format(date)
      // Удаляем ' .г' в конце строки
      return formattedDate.slice(0, formattedDate.length - 3)
    },
    orderTime() {
      const options = { hour: 'numeric', minute: 'numeric' }
      const date = new Date(this.order.datetime)

      return new Intl.DateTimeFormat('ru-RU', options).format(date)
    },
    receiverText() {
      const nameSplit = this.order.receiver.fullName.split(' ')
      const name = `${nameSplit[1]} ${nameSplit[0]}`

      const phone = this.order.receiver.phoneNumber
      const phoneNumber = phone.substring(0, 4) + '****' + phone.substring(9)

      return `${name} ${phoneNumber}`
    }
  }
}
</script>

<style lang="scss" scoped>
.card-content {
  gap: 18px;
}

.order-image {
  width: 64px;
  height: 64px;
}

.order-title {
  line-height: 16px;
}

.order-vendor-code {
  font-size: 12px;
  line-height: 12px;
  color: $primary;
}
</style>