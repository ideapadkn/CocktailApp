<script setup>
import axios from "axios";
import { computed, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import { COCKTAILS_BY_ID } from "../constants";
import AppLayout from "../components/AppLayout.vue";

const route = useRoute();
const router = useRouter();

const cocktail = ref(null);
const cocktailId = computed(() => route.path.split("/").pop());

async function getCocktail() {
  const data = await axios.get(`${COCKTAILS_BY_ID}${cocktailId.value}`);
  cocktail.value = data?.data?.drinks[0];
}
getCocktail();
</script>

<template>
  <div v-if="cocktail" class="wrap">
    <AppLayout :imgUrl="cocktail.strDrinkThumb">
      <div class="wrapper">
        <div class="info">
          <div class="title">{{ cocktail.strDrink }}</div>
          <div class="line"></div>
          <div class="ingresients">
            <div>
              <ul>
                <template v-for="(el, index) of new Array(20)">
                  <li
                    class="first-li"
                    v-if="cocktail[`strIngredient${index + 1}`]"
                  >
                    {{ cocktail[`strIngredient${index + 1}`] }}
                  </li>
                </template>
              </ul>
            </div>
            <div>
              <ul>
                <template v-for="(el, index) of new Array(20)">
                  <li v-if="cocktail[`strMeasure${index + 1}`]">
                    | {{ cocktail[`strMeasure${index + 1}`] }}
                  </li>
                </template>
              </ul>
            </div>
          </div>
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
  .first-li::before
    content: url(../assets/img/li-heart.png)
    position: absolute
    left: -30px
.ingresients
  display: flex
  text-align: left
  margin-bottom: 80px
.btn
  position: absolute
  top: 32px
  left: 40px
.description
  color: $textMuted
  font-family: Raleway
  font-size: 20px
  font-style: normal
  font-weight: 400
  line-height: 30px
  letter-spacing: 2px
</style>
