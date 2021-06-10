<template>
  <div class="check-list">
      <div class="check-list__container">
         <div class="check-list__item">
          <label class="check-list__item-checkbox" >
              <svg width="12" :class="{'rotated':isShowed}" height="12" viewBox="0 0 16 28" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M1.77783 26.4444L14.2223 14L1.77783 1.55554" stroke="#1A0A03" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
              <input class="check-list__custom-checkbox" type="checkbox" :checked="isShowed" @input="handleChange"/>
              <span class="check-list__item-name">{{name}}</span>
          </label>
          <div  v-if="isShowed && chars && chars.length" class="check-list__item-chars">
              <div class="check-list__item-char" v-for="char in chars" :key="char.id">
                <label class="check-list__item-char-switch">
                <input type="checkbox" @input="handleChangeCharActivity(char.id)" :checked="char.isActive" />
              </label>
              <div class="check-list__item-char-name">{{char.name}}</div>
              <div class="check-list__item-char-val">
              <span>{{char.value}}</span>
              <div class="check-list__item-char-color" :style="{backgroundColor:char.color}"></div></div>
              </div>
          </div>
          <div v-if="isShowed && chars &&  !chars.length" class="check-list__empty-set">
            У данного продукта нет характеристик
          </div>
        </div>
      </div>
  </div>
</template>
<script>
export default {
  name:'ListComponent',
  props:{
    id: Number,
    name: String,
    isShowed: Boolean,
    chars:Array,
  },
  methods:{
    handleChangeCharActivity(charId){
      // передаем родителю id продукта и хараткеристики
      this.$emit('handleCharClick', {productId: this.id, charId});
    },
    handleChange(){
      this.$emit('handleClick', this.id);
    }
  },
}
</script>
<style lang="sass" scoped>
.check-list
    &__empty-set
        color: red
        font-size: 14px
    &__custom-checkbox
      position: absolute
      left: -9999px
    &__item
        min-width: 276px
    &__item-char-name
        flex: 1
        flex-basis: 70%
        margin-right: 5rem
    &__item-char-val
        display: flex
        gap: 0.2rem
    &__title
    &__item-checkbox
        display: flex
        align-items: center
        gap: 0.5rem
          
    &__item-chars
        padding-left: 20px
    &__item-char
        gap: 0.2rem 
        display: flex
        margin-bottom: 0.6rem
        align-items: center
    &__item-char-color
        width: 20px
        height: 20px
.rotated
  transform: rotate(90deg)
</style>