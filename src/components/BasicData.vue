<template>
    <div v-if="currentData" class="w-100 p-3 text-light">
        <h1 class="display-3 mb-0">{{ currentTemperature }}°C</h1>
        <span class="text-light opacity-75">{{ currentData.weather[0].description }}</span>

    </div>

    <!-- <h6 class="display-7 m-3">{{ getDate(currentData.dt) }}</h6> -->
    <div class="h-100 w-100 p-3 d-flex flex-row">
        <div class="card bg-dark m-2" style="text-align: center;">
            <div class="card-body">
                <span class="text-white-50">24 Saat   </span><span>13:00</span>
                <p>24°C</p>
            </div>
            <img src="@/assets/sun.png" alt="sun" class="mx-auto" style="height: 75px;">
        </div>
        <div class="card bg-dark m-2" style="text-align: center;">
            <div class="card-body">
                <span class="text-white-50">24 Saat   </span><span>13:00</span>
                <p>24°C</p>
            </div>
            <img src="@/assets/sun.png" alt="sun" class="mx-auto" style="height: 75px;">
        </div>
        <div class="card bg-dark m-2" style="text-align: center;">
            <div class="card-body">
                <span class="text-white-50">24 Saat   </span><span>13:00</span>
                <p>24°C</p>
            </div>
            <img src="@/assets/sun.png" alt="sun" class="mx-auto" style="height: 75px;">
        </div>
        <div class="card bg-dark m-2" style="text-align: center;">
            <div class="card-body">
                <span class="text-white-50">24 Saat   </span><span>13:00</span>
                <p>24°C</p>
            </div>
            <img src="@/assets/sun.png" alt="sun" class="mx-auto" style="height: 75px;">
        </div>
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