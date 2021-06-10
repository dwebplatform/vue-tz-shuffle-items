<template>
<div class="list-dashboard">
    <div v-for="product in showedProducts(products)" :key="product.id" class="list-dashboard__item">
      <div class="list-dashboard__item-top">
        <div class="list-dashboard__item-name">
          {{product.name}}
        </div>
        <button class="list-dashboard__shuffle-btn"
        @click="toggleShuffled"
        >{{isShuffled ? 'Отсортировать':'Перемешать'}}</button>
      </div>
      <div   class="list-dashboard__ordered-items">
        <div v-for="char in activeChars(product)" :key="char.id"  class="list-dashboard__ordered-item">
          <div v-if="!isShuffled" class="list-dashboard__ordered-item-active-char">
            <div v-for="index in new Array(char.value)" :key="index" class="list-dashboard__char-box"
              :style="{backgroundColor: char.color}"
            />
          </div>
        </div>   
        <div v-if="isShuffled" class="list-dashboard__ordered-item-shuffled-char">
        <div v-for="(color,index) in shuffledActiveChars(product)" :key="index" 
         class="list-dashboard__char-box"
            :style="{backgroundColor: color}"
        ></div>
        </div> 
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name:'ListDashBoard',
  props: {
    products: Array
  },
  methods: {
    shuffleArray(array){
      return array.sort(() => 0.5 - Math.random())
    },
    toggleShuffled(){
      this.isShuffled = !this.isShuffled;
    },
    shuffledActiveChars(product){
        const activeChars = this.activeChars(product);
        let shuffledChars = [];
        activeChars.forEach(({value, color})=>{
          console.log(value,color)
          let coloriesedArray = [...new Array(value)].map(()=>color);
          shuffledChars =  shuffledChars.concat(coloriesedArray);
        }) 
        return this.shuffleArray(shuffledChars);
    },
    activeChars(product){
        if(!product.chars){
          return [];
        }
        return product.chars.filter((char=>char.isActive ))
      },
      showedProducts(products){
        return products.filter(p=>p.isShowed)
      }
  },
 
  data(){
    return {
      isShuffled: false,
      name:'Лист 2',
      isShowed: false,
        items:[{
          id:1,
          name:'Характеристика 1',
          value: 6,
          color: 'red',
          isActive: true
        },
        {
          id:2,
          name:'Характеристика 2',
          value: 14,
          color: 'green',
          isActive: false
        },
        {
          id:3,
          name:'Характеристика 3',
          value: 4,
          color: 'yellow',
          isActive: false
        },
        {
          id:4,
          name:'Характеристика 4',
          value: 4,
          color: 'green',
          isActive: false
        },
         {
          id:5,
          name:'Характеристика 5',
          value: 12,
          color: 'brown',
          isActive: false
        },
         {
          id:6,
          name:'Характеристика 6',
          value: 7,
          color: 'red',
          isActive: false
        }
        ]
      }
    }
}
</script>
<style lang="sass" scoped>
.list-dashboard
    display: flex
    width: 100%
    flex-flow: column
    padding: 20px
    gap: 1rem
    &__shuffle-btn
        padding: 0.5rem 1rem
        border: none
        font-size: 14px
        border-radius: 15px
        background-color: skyblue
        color: #fff
        cursor: pointer
    &__item
    &__item-top
        display: flex
        justify-content: space-between
    &__ordered-item-active-char
        width: 100%
        display: flex
        margin-bottom: 8px
    &__ordered-item-shuffled-char
        width: 100%
        display: flex
    &__char-box
        width: 10px
        height: 10px
        margin-right: 2px
    
</style>