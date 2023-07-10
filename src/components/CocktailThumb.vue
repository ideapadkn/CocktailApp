<script setup>
  import { defineProps } from 'vue';

  const props = defineProps({
    cocktail: {
      type: Object,
      required: true
    }
  })
</script>

<template>
  <div class="root">
    <RouterLink :to="`/cocktails/${cocktail.idDrink}`">
      <div :style="`background-image: url(${cocktail.strDrinkThumb})`" class="pic"></div>
    </RouterLink>
    <div class="name">
      {{ cocktail.strDrink }}
    </div>
  </div>
</template>

<style lang="sass" scoped>
  @import '../assets/styles/main'
  .root 
    width: calc(( 100% - 76px )/3)
    margin-right: 25px
    padding-bottom: 20px
    &:nth-child(3n + 3)
      padding-right: 0
      
  .pic
    height: 120px
    width: 120px
    margin: 0 auto
    background-repeat: no-repeat
    background-position: 50% 50%
    background-size: 100%
    margin-bottom: 15px
  .btn
    position: absolute
    top: 32px
    left: 40px
  .name 
    width: 100%
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    font-size: 16px
    font-style: normal
    font-weight: 400
    line-height: normal
    letter-spacing: 1.6px
</style>