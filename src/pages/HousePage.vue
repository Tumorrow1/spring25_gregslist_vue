<script setup>
import { AppState } from '@/AppState.js';
import HouseForm from '@/components/HouseForm.vue';
import HouseListing from '@/components/HouseListing.vue';
import { housesService } from '@/services/HousesService.js';
import { logger } from '@/utils/Logger.js';
import { Pop } from '@/utils/Pop.js';
import { computed, onMounted } from 'vue';

const Houses = computed(() => AppState.houses)

onMounted(() => {
  getHouses()
})

async function getHouses() {
  try {
    await housesService.getHouses()
  } catch (error) {
    Pop.error(error, `got no house boi`)
    logger.log(`no house man`, error)
  }
}
</script>


<template>
  <section class="container">
    <div class="row">
      <div class="col-12">
        <div class="text-center">
          <h1 class="display-3">Houses</h1>
        </div>
      </div>
    </div>
  </section>
  <section class="container">
    <div class="row">
      <div class="col-md-6">
        <HouseForm />
      </div>
      <div class="col-md-6 my-3">
        <div class="text-center">
          <img
            src="https://images.unsplash.com/photo-1562095281-65d72e33b239?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8c2hhcXxlbnwwfHwwfHx8MA%3D%3D"
            alt="shaq singing">
        </div>
      </div>
    </div>
  </section>
  <section class="container">
    <div class="row">
      <div v-for="house in Houses" :key="house.id" class="col-12">
        <HouseListing :house-prop="house" />
      </div>
    </div>
  </section>
</template>



<style lang="scss" scoped></style>