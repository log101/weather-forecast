<template>
    <div v-if="currentData" class="w-100 p-3 text-light">
        <h1 class="display-3 mb-0">{{ currentTemperature }}°C</h1>
        <span class="text-light opacity-75">{{ currentData.weather[0].description }}</span>
        
    </div>
    <div style="background-color: black;" class="mx-auto">

        <!-- <h6 class="display-7 m-3">{{ getDate(currentData.dt) }}</h6> -->
        <h6 class="display-7 m-3">asşdmas</h6>
        <h6 class="display-6 b-3">24°C</h6>
        <img src="@/assets/sun.png" alt="sun" class="mx-auto" style="height: 100px;">
    </div>
</template>

<script>

export default {
    props: {
        currentData: Object, 
    },
    computed: {
        currentTemperature() { 
            return Math.round(this.currentData.main.temp)
        }
    }
}
</script>

<style scoped>

</style>