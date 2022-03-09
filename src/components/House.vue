<template>
    <router-link :to="{name: 'HouseDetails', params: {id: house.id}}">
    <div class="house row p-3 bg-white rounded shadow selectable">
        <div class="col-12">
            <img class="img-fluid" :src="house.imgUrl" alt="" />
        </div>
        <h3 class="text-center col-12">
            {{house.bedrooms}} | {{house.bathrooms}} | {{house.year}}
        </h3>
        <!-- <div class="col-12">
      <p>{{ house.description }}</p>
      <p>{{ house.price }}</p>
      <p>{{ house.levels }}</p>
    </div> -->

    </div>

    </router-link>
</template>


<script>
export default {
    props: {
        house:{
            type: Object,
            required: true 
        },
    },
    setup(){
        return {}
    }
}
</script>


<style lang="scss" scoped>

</style>