<template>
    <div class="container-fluid">
        <div class="row">
            <div v-for="h in houses" :key="h.id" class="col-4 p-4 mb-2">
        <House :house = "h"/>
            </div>
        </div>

    </div>
</template>


<script>
import { computed, onMounted } from '@vue/runtime-core'
import Pop from '../utils/Pop'
import { housesService } from '../services/HousesService'
import { logger } from '../utils/Logger'
import { AppState } from '../AppState'
export default {
    setup(){
        onMounted(async () => {
            try {
                await housesService.getAll()
            } catch (error) {
                Pop.toast(error.message, 'error')
                logger.error(error)
            }
        })
        return {
            houses: computed(() => AppState.houses)
        }
    }
}
</script>


<style lang="scss" scoped>

</style>