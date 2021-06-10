<template>
  <main class="main">
    <div class="main__aside">
      <ListComponent
        v-for="product in products"
        :key="product.id"
        :name="product.name"
        :isShowed="product.isShowed"
        :chars="product.chars"
        :id="product.id"
        @handleClick="handleIsShowed"
        @handleCharClick="handleCharClick"
      />
    </div>
    <div class="other">
      <ListDashBoard :products="products"/>
    </div>
  </main>
</template>

<script>
import ListComponent from "./components/ListComponent";
import ListDashBoard from "./components/ListDashBoard";
export default {
  name: "App",
  methods: {
    getProdById(id) {
      const findedProduct = this.products.find(p => p.id == id);
      if (!findedProduct) {
        return null;
      }
      return findedProduct;
    },
    handleCharClick({ productId, charId }) {
      if (!this.getProdById(productId)) {
        return;
      }
      const { chars } = this.getProdById(productId);
      chars.find(char=>char.id===charId).isActive = !chars.find(char=>char.id===charId).isActive;
      this.getProdById(productId).chars = chars;
    },
    handleIsShowed(productId) {
      if (!this.getProdById(productId)) {
        return;
      }
      this.products.find(p => p.id == productId).isShowed = !this.products.find(
        p => p.id == productId
      ).isShowed;
    }
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Продукт 1",
          isShowed: true,
          chars: [
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "red",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "green",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "yellow",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "green",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "brown",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "red",
              isActive: false
            }
          ]
        },
        {
          id: 2,
          isShowed: false,
          name: "Продукт 2",
          chars:[
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "red",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "green",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "yellow",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "green",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "brown",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "red",
              isActive: false
            }
          ]
        },
        {
          id: 3,
          isShowed: false,
          name: "Продукт 3",
          chars: [
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "red",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "green",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "yellow",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "green",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "brown",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "red",
              isActive: false
            }
          ]
        },
        {
          id: 4,
          isShowed: false,
          name: "Продукт 4",
          chars: [
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "red",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "green",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "yellow",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "green",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "brown",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "red",
              isActive: false
            }
          ]
        }
      ]
    };
  },
  components: {
    ListComponent,
    ListDashBoard
  }
};
</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100&display=swap')
*
    box-sizing: border-box
    margin: 0
    padding: 0
    font-family: 'Montserrat', sans-serif

.main
  padding: 20px
  display: flex
  gap: 1rem
  &__aside
.other
    flex:1
    border: 1px solid red
    border-radius: 6px
</style>
