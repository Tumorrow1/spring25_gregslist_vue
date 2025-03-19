<script setup>
import { housesService } from '@/services/HousesService.js';
import { logger } from '@/utils/Logger.js';
import { Pop } from '@/utils/Pop.js';
import { Value } from 'sass';
import { ref } from 'vue';



const editableHouseData = ref({
  bedrooms: 0,
  bathrooms: 0,
  price: 0,
  year: 1,
  imgUrl: ``,
  levels: 0,

})
async function createHouse() {
  try {
    const houseData = editableHouseData.value
    await housesService.createHouse(houseData)
    editableHouseData.value = {
      bedrooms: 0,
      bathrooms: 0,
      price: 0,
      year: 1,
      imgUrl: ``,
      levels: 0

    }
  } catch (error) {
    Pop.error(error, `couldnt create house`)
    logger.log(`No create house son`, error)
  }
}
</script>


<template>
  <form @submit.prevent="createHouse()">
    <div class="mb-3">
      <label for="houseBedrooms">Bedrooms</label>
      <input v-model="editableHouseData.bedrooms" id="houseBedrooms" name="bedrooms" type="number" required
        maxlength="500" placeholder="Bedrooms...">
    </div>
    <div class="mb-3">
      <label for="houseBathrooms">Bathrooms</label>
      <input v-model="editableHouseData.bathrooms" id="houseBathrooms" name="Bathrooms" type="number" required
        maxlength="500" placeholder="Bathrooms...">
    </div>
    <div class="mb-3">
      <label for="housePrice">Price</label>
      <input v-model="editableHouseData.price" id="housePrice" name="Price" type="number" required maxlength="500"
        placeholder="Price...">
    </div>
    <div class="mb-3">
      <label for="houseimgUrl">imgUrl</label>
      <input v-model="editableHouseData.imgUrl" id="houseimgUrl" name="imgUrl" type="url" required maxlength="500"
        placeholder="imgUrl...">
    </div>
    <div class="mb-3">
      <label for="houseYear">Year</label>
      <input id="houseYear" name="Year" type="text" required maxlength="500" placeholder="Year...">
    </div>
    <div class="mb-3">
      <label for="houselevels">levels</label>
      <input v-model="editableHouseData.levels" id="houselevels" name="levels" type="number" required maxlength="500"
        placeholder="levels...">
    </div>
    <div class="text-end">
      <button class="btn btn-outline-success" type="submit">
        submit
      </button>
    </div>
  </form>
</template>


<style lang="scss" scoped></style>