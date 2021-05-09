<template>
  <v-row justify="center" align="center">
    <v-col v-for="(pizza, index) in pizzas" :key="index" cols="12" sm="4">
      <v-card class="pa-3">
        <v-card-title>{{ pizza.name }} - ${{ pizza.price }}</v-card-title>
        <v-btn
          min-width="100%"
          :color="butHandler(pizza.isSelected)"
          @click="selectHandler('pizzas', index)"
          >SELECT</v-btn
        >
      </v-card>
    </v-col>
    <v-col cols="12">
      <v-card class="pa-3">
        <v-card-title>Size</v-card-title>
        <div class="d-flex justify-center">
          <v-btn
            v-for="(size, index) in sizes"
            :key="index"
            :color="butHandler(size.isSelected)"
            @click="selectHandler('sizes', index)"
            >{{ size.name }}</v-btn
          >
        </div>
      </v-card>
    </v-col>
    <v-col cols="12">
      <v-card class="pa-3">
        <v-card-title>Toppings</v-card-title>
        <v-row class="px-10">
          <v-col cols="3" v-for="(item, index) in toppings" :key="index">
            <v-checkbox
              :disabled="disHandler(item.avail)"
              color="success"
              :label="item.name"
              v-model="item.isSelected"
            ></v-checkbox>
          </v-col>
        </v-row>
      </v-card>
    </v-col>
    <v-col cols="12">
      <v-card class="pa-3">
        <v-card-title class="justify-center"
          ><h1>Total Price: ${{ totalPrice }}</h1>
        </v-card-title>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo,
  },
  computed: {
    totalPrice() {
      let price = 0
      this.pizzas.forEach((el) => {
        if (el.isSelected === true) {
          price += el.price
        }
      })
      this.sizes.forEach((el) => {
        if (el.isSelected === true) {
          price += el.price
        }
      })
      this.toppings.forEach((el) => {
        if (el.isSelected === true) {
          price += el.price
        }
      })
      return price
    },
  },
  methods: {
    disHandler(data) {
      const tes = this.pizzas.findIndex((el) => el.isSelected === true)
      if (data[tes] === 0) {
        return true
      } else {
        return false
      }
    },
    butHandler(isSelected) {
      if (isSelected === true) {
        return 'success'
      } else {
        return ''
      }
    },
    selectHandler(data, index) {
      switch (data) {
        case 'pizzas':
          this.pizzas.map((el) => (el.isSelected = false))
          this.toppings.map((el) => (el.isSelected = false))
          this.pizzas[index].isSelected = true
          break
        case 'sizes':
          this.sizes.map((el) => (el.isSelected = false))
          this.sizes[index].isSelected = true
          break

        default:
          break
      }
    },
  },
  data() {
    return {
      pizzas: [
        { name: 'Pizza A', price: 8, isSelected: true },
        { name: 'Pizza B', price: 10, isSelected: false },
        { name: 'Pizza C', price: 12, isSelected: false },
      ],
      sizes: [
        { name: 'Small', price: -1, isSelected: false },
        { name: 'Medium', price: 0, isSelected: true },
        { name: 'Large', price: 2, isSelected: false },
      ],
      toppings: [
        { name: 'Avocado', price: 1, isSelected: false, avail: [1, 0, 0] },
        { name: 'Lobster', price: 2, isSelected: false, avail: [0, 1, 0] },
        { name: 'Bacon', price: 3, isSelected: false, avail: [0, 1, 1] },
        { name: 'Broccoli', price: 1, isSelected: false, avail: [1, 1, 1] },
        { name: 'Oyster', price: 2, isSelected: false, avail: [0, 1, 0] },
        { name: 'Duck', price: 3, isSelected: false, avail: [0, 0, 1] },
        { name: 'Onions', price: 1, isSelected: false, avail: [1, 1, 1] },
        { name: 'Salmon', price: 2, isSelected: false, avail: [0, 1, 0] },
        { name: 'Ham', price: 3, isSelected: false, avail: [1, 1, 1] },
        { name: 'Zucchini', price: 1, isSelected: false, avail: [1, 1, 1] },
        { name: 'Tuna', price: 2, isSelected: false, avail: [1, 0, 1] },
        { name: 'Sausage', price: 3, isSelected: false, avail: [0, 0, 1] },
      ],
    }
  },
}
</script>
