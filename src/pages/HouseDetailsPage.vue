<template>
    <div class="container">
        <div class="row mt-3 bg-light shadow p-4">
            <div class="col-md-6">
                <img :src="house.imgUrl" class="img-fluid">
            </div>
            <div class="col-md-6">
                <h1>{{ house.bedrooms }} | {{ house.bathrooms }}</h1>
        <h2>{{ house.year }}</h2>
        <p>{{ house.description }}</p>
        <b>{{ house.price }}</b>
         <div class="text-end selectable" @click="openModal">
          Edit House
          <i class="mdi mdi-pencil"></i>
        </div>
            </div>
        </div>
        <Modal>
        <template #modal-title>Edit {{ house.bedrooms }} {{ car.model }}</template>
      <template #modal-body><CarForm :houseData="house" /></template>
        </Modal>

    </div>
</template>


<script>
import { computed, onMounted } from '@vue/runtime-core'
import Pop from '../utils/Pop'
import { AppState } from '../AppState'
import { useRoute } from 'vue-router'
import { logger } from '../utils/Logger'
import { housesService } from '../services/HousesService'
export default {
    setup(){
        const route = useRoute();
        onMounted(async () => {
            try {
                AppState.activeHouse = {}
                logger.log(route.params);
                await housesService.getById(route.params.id);
            } catch (error) {
                logger.error(error)
                Pop.toast(error.message, 'error')
            }
        })
        return {
            house: computed(() => AppState.activeHouse)
        }
    }
}
</script>


<style lang="scss" scoped>

</style>