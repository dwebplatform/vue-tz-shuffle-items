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
        :isAllChecked="true"
        @handleColorChange="handleColorChange"
        @handleValueChange="handleValueChange"
        :parentCheckBox="getParentCheckBox(product)"
        @handleClick="handleIsShowed"
        @handleCharClick="handleCharClick"
        @handleToggleAllClick="handleToggleAllClick"
      />
    </div>
    <div class="other">
      <ListDashBoard @handleToggleShuffled="handleToggleShuffled" :products="products"/>
    </div>
  </main>
</template>

<script>
import ListComponent from "./components/ListComponent";
import ListDashBoard from "./components/ListDashBoard";
export default {
  name: "App",
  methods: {
    shuffleArray(array){
      return array.sort(() => 0.5 - Math.random())
    },
     activeChars(product){
        if(!product.chars){
          return [];
        }
        return product.chars.filter((char=>char.isActive ))
      },
    handleToggleShuffled(productId){
      if(!this.getProdById(productId)){
          return;
        }
        this.getProdById(productId).isShuffled =!this.getProdById(productId).isShuffled;
        const product = this.getProdById(productId);
        const activeChars = this.activeChars(product);
        let shuffledChars = [];
        activeChars.forEach(({value, color})=>{
          let coloriesedArray = [...new Array(value)].map(()=>color);
          shuffledChars =  shuffledChars.concat(coloriesedArray);
        }); 
          this.getProdById(productId).shuffledChars = this.shuffleArray(shuffledChars);


    },
    handleColorChange({productId, charId,colorValue}){
      if(!this.getProdById(productId)){
          return;
        }
        const { chars } =this.getProdById(productId);
        chars.find(c=>c.id==charId).color = colorValue ;
        this.getProdById(productId).chars = chars;
    },
    handleValueChange({productId, charId,charValue}){
        if(!this.getProdById(productId)){
          return;
        }
        const { chars} =this.getProdById(productId);
        chars.find(c=>c.id==charId).value = parseInt(charValue);
        this.getProdById(productId).chars = chars;
    },
    getParentCheckBox(product){
      if(!product.chars){
        return 'allUnCheked';
      }
      const { chars } =product;
      const activeCharCount = chars.filter(c=>c.isActive).length;

      if(activeCharCount === chars.length){
        return 'allChecked';
      }  else if(activeCharCount>0 && activeCharCount <chars.length){
        return 'partialChecked';
      } else {
        
         return 'allUnCheked';
      }
    },
    getProdById(id) {
      const findedProduct = this.products.find(p => p.id == id);
      if (!findedProduct) {
        return null;
      }
      return findedProduct;
    },

    handleToggleAllClick(productId){
      // pass state
       const { chars } = this.getProdById(productId);
       if(!chars||!chars.length){
         return;
       }
       let countOfActiveChars = chars.filter(c=>c.isActive===true).length;
       if(countOfActiveChars===0){
        this.getProdById(productId).chars = chars.map((c)=>{
          c.isActive = true;
          return c;
        })
       }  else if(countOfActiveChars>0 &&countOfActiveChars<chars.length) {
       this.getProdById(productId).chars = chars.map((c)=>{
          c.isActive = true;
          return c;
        })
       } else {
          this.getProdById(productId).chars = chars.map((c)=>{
          c.isActive = false;
          return c;
        });

       }
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
          isShuffled: false,
          shuffledChars:[],
          chars: [
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "#ff0000",
              isActive: false
            }
          ]
        },
        {
          id: 2,
          isShowed: false,
          name: "Продукт 2",
          isShuffled: false,
           shuffledChars:[],
          chars:[
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "#ff0000",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "#ff0000",
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
              color: "#ff0000",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "#ff0000",
              isActive: false
            }
          ]
        },
        {
          id: 3,
          isShowed: false,
          name: "Продукт 3",
          isShuffled: false,
           shuffledChars:[],
          chars: [
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "#ff0000",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "#ff0000",
              isActive: false
            }
          ]
        },
        {
          id: 4,
          isShowed: false,
          name: "Продукт 4",
          isShuffled: false,
           shuffledChars:[],
          chars: [
            {
              id: 1,
              name: "Характеристика 1",
              value: 6,
              color: "#ff0000",
              isActive: true
            },
            {
              id: 2,
              name: "Характеристика 2",
              value: 14,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 3,
              name: "Характеристика 3",
              value: 4,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 4,
              name: "Характеристика 4",
              value: 4,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 5,
              name: "Характеристика 5",
              value: 12,
              color: "#ff0000",
              isActive: false
            },
            {
              id: 6,
              name: "Характеристика 6",
              value: 7,
              color: "#ff0000",
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
