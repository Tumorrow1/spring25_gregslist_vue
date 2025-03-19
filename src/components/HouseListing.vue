<script setup>
import { House } from '@/models/House.js';

defineProps({
  houseProp: { type: House, required: true }
})
</script>


<template>
  <div class="row shadow-lg">
    <div class="col-5 my-3">
      <img :src="houseProp.imgUrl" :alt="`a pictuer of ${houseProp.price}${houseProp.year}`" class="img-fluid">
    </div>
    <div class="col-md-7 ">
      <div class="p-3">
        <div class="justify-content-between d-flex">
          <p class="fs-4 gap-3"> Year: {{ houseProp.year }} | Bedrooms: {{ houseProp.bedrooms }} | Bathrooms: {{
            houseProp.bathrooms }}</p>
          <small>{{ houseProp.createdAt.toLocaleDateString() }}</small>
        </div>
        <div>
          <p class="fs-3">{{ `$` + houseProp.price.toLocaleString() }}</p>
          <p>{{ houseProp.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>



<style lang="scss" scoped></style>