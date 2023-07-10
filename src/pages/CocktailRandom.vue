<script setup>
import axios from 'axios';
import { computed, ref } from 'vue';
import { useRoute,useRouter } from 'vue-router';
import { COCKTAILS_RANDOM, INGREDIENT_PIC } from '../constants'
import AppLayout from '../components/AppLayout.vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

const route = useRoute()
const router = useRouter()

const cocktail = ref(null)

async function getCocktail() {
  const data = await axios.get(COCKTAILS_RANDOM)
  cocktail.value = data?.data?.drinks[0]
}
getCocktail()
</script>

<template>
  <div v-if="cocktail" class="wrap">
    <AppLayout :imgUrl="cocktail.strDrinkThumb">
      <div class="wrapper">
        <div class="info">
          <div class="title">{{ cocktail.strDrink }}</div>
          <swiper
            :slides-per-view="3"
            :space-between="50"
            class="swiper"
          >
            <swiper-slide
              v-for="(el, index) of new Array(20)"
              :key="el"
            >
              <img :src="`${INGREDIENT_PIC}${el}-Small.png`" alt="">
              <p class="first-li" v-if="cocktail[`strIngredient${index + 1}`]">
                {{ cocktail[`strIngredient${index + 1}`] }} 
              </p>
            </swiper-slide>
          </swiper>
          <div class="description">
            {{ cocktail.strInstructions }}
          </div>
        </div>
      </div>
    </AppLayout>
  </div>

</template>

<style lang="sass" scoped>
@import '../assets/styles/main'
.wrapper 
  display: flex
  justify-items: center
  align-items: center
  flex-wrap: wrap
.info
  padding: 80px 0
  text-align: center
  margin: 0 auto
.title
  margin-bottom: 50px
.swiper
  margin-bottom: 50px
  width: 360px
ul
  list-style: none
  li 
    font-family: Raleway
    font-size: 18px
    font-style: normal
    font-weight: 400
    line-height: 27px
    letter-spacing: 1.8px
    margin-bottom: 20px
    position: relative
.description
  color: $textMuted
  font-family: Raleway
  font-size: 20px
  font-style: normal
  font-weight: 400
  line-height: 30px
  letter-spacing: 2px
@media screen and (max-width: 750px)
  .swiper 
    width: 300px
</style>