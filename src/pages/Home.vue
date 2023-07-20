<script setup>
import AppLayout from '../components/AppLayout.vue';
import CocktailThumb from '../components/CocktailThumb.vue'
import { useRootStore } from '../stores/root'
import { storeToRefs } from 'pinia';

const rootStore = useRootStore()
rootStore.getIngredients()

const { ingredients, ingredient, cocktails } = storeToRefs(rootStore)


function getCocktails() {
  rootStore.getCocktails(rootStore.ingredient)
}

function removeIngredient() {
  rootStore.setIngredient(null)
}
</script>

<template>
  <AppLayout imgUrl="/src/assets/img/1.png" :backFunc="removeIngredient" :is-back-button-visible="!!ingredient"> 
    <div class="wrapper">
      <div v-if="!ingredient || !cocktails" class="info">
        <div class="title">Choose Your Drink</div>
        <div class="line"></div>
        <div class="select-wrapper">
          <el-select 
            v-model="rootStore.ingredient" 
            placeholder="Choise Main Ingredient" 
            size="large"
            filterable
            allow-create
            class="select"
            @change="getCocktails"
          >
            <el-option
              v-for="item in ingredients"
              :key="item.strIngredient1"
              :label="item.strIngredient1"
              :value="item.strIngredient1"
            />
          </el-select>
        </div>
        <div class="text">
          Try our delicious cocktail recipes for every occasion. Find delicious cocktail recipes by ingredient through our cocktail generator.
        </div>
        <img src="../assets/img/2.png" alt="Cocktails" class="img">
      </div>
      <div v-else class="info">
        <div class="title">cocktails with {{ ingredient }}</div>
        <div class="line"></div>
        <div class="cocktails">
          <CocktailThumb 
            v-for="cocktail in cocktails" 
            :key="cocktail.idDrink"
            :cocktail="cocktail"
          />
        </div>
      </div>
    </div>
  </AppLayout>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'
.wrapper 
  display: flex
  justify-items: center
  align-items: center
.info
  padding: 80px 0
  text-align: center
  margin: 0 auto
.select-wrapper 
  margin-bottom: 50px
.select 
  width: 220px
.text
  max-width: 516px
  color: $textMuted
  font-family: Raleway
  font-size: 16px
  font-style: normal
  font-weight: 400
  line-height: 36px
  letter-spacing: 1.6px
  margin-bottom: 60px
.cocktails
  display: flex
  align-items: center
  margin-top: 60px
  flex-wrap: wrap
  max-height: 400px
  overflow-y: auto
  
</style> 