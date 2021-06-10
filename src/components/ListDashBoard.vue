<template>
<div class="list-dashboard">
    <div v-for="product in showedProducts(products)" :key="product.id" class="list-dashboard__item">
      <div class="list-dashboard__item-top">
        <div class="list-dashboard__item-name">
          {{product.name}}
        </div>
        <button class="list-dashboard__shuffle-btn"
        @click="toggleShuffled(product.id)"
        >{{product.isShuffled ? 'Отсортировать':'Перемешать'}}</button>
      </div>
      <div   class="list-dashboard__ordered-items">
        <div v-for="char in product.chars.filter((c)=>c.isActive)" :key="char.id"  class="list-dashboard__ordered-item">
          <div v-if="!product.isShuffled" class="list-dashboard__ordered-item-active-char">
            <div v-for="index in getArrayFromChar(char)" :key="index" class="list-dashboard__char-box"
              :style="{backgroundColor: char.color}"
            />
          </div>
        </div>  
        <div v-if="product.isShuffled" class="list-dashboard__ordered-item-shuffled-char">
        <div v-for="(color,index) in product.shuffledChars" :key="index" 
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
    getArrayFromChar(char){
      if(!char.value){
        return [];
      }
      return new Array(char.value);
    },
    toggleShuffled(productId){
      this.$emit('handleToggleShuffled',productId);
      // this.isShuffled = !this.isShuffled;
    },
    activeChars(product){
        if(!product.chars ||!product.chars.length){
          return false;
        }

        return product.chars.filter((char=>char.isActive )).length>0? true: false;
      },
      showedProducts(products){
        
        return products.filter(this.activeChars);
      }
  },
 
  data(){
    return {}
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
        padding-top: 5px
        display: flex
        flex-wrap: wrap
        gap: 1px
    &__char-box
        width: 10px
        height: 10px
        margin-right: 2px
    
</style>