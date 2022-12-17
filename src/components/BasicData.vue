<template>
    <div v-if="currentData" class="w-100 p-3 text-light">
        <h1 class="display-3 mb-0">{{ currentTemperature }}°C</h1>
        <span class="text-light opacity-75">{{ currentData.weather[0].description }}</span>

    </div>
    <!-- 
        Burada v-if direktifini kullanmak zorundayız, öbür türlü veriyi daha tamamlanmadan
        kullanmaya çalışır ve uygulama hata verir
    -->
    <div v-if="dailyData" class="container-fluid">
        <div class="h-100 p-3 d-flex flex-row flex-nowrap" style="overflow-x: auto;">
            <!--
                v-for ile template içerisinde bir döngü oluşturuyoruz, mapDailyDataWeatherInfo API'den
                JSON yanıtının yalnızca bizim kullanacağımız alanlarını bir nesne içerisinde veriyor ve saatlik
                dilimler halinde gelen verileri Bootstrap cardları şeklinde temsil ediyoruz.
                
                API 5 günlük hava durumu verisini 3 saatlik dilimler halinde veriyor, dikkat edilmesi gereken nokta
                hava durumlarını talebin yapıldığı saatten itibaren veriyor, yani saat 17.00'da talepte bulunduysanız
                içinde bulunduğunuz gün için yalnızca 18.00 21.00 ve 24.00'deki hava durumları verinin içerisinde bulunuyor
                veriyi günlere parçalarken buna dikkat edin.
            -->
            <template v-for="hourlyData in mapDailyDataToWeatherInfo" :key="hourlyData.date">
                <div class="card bg-dark m-2 col-3" style="text-align: center;">
                    <div class="card-body">
                        <span class="text-white-50">24 Saat </span><span>{{ hourlyData.date }}</span>
                        <p>{{ hourlyData.temperature }}°C</p>
                        <p>{{ hourlyData.description }}</p>
                    </div>
                    <!-- 
                        img etiketinin src niteliğini bir fonsiyon sonucu olarak aldığımız için doğrudan
                        veremiyoruz, v-bind direktifini kullanmamız gerekiyor
                    -->
                    <img v-bind:src="hourlyData.icon" alt="sun" class="mx-auto" style="height: 75px;">
                </div>
            </template>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        currentData: Object,
        dailyData: Object
    },
    // Computed kısmında belirli bir işlem gerektiren verileri tutuyoruz
    // BURADAKİ METODLARI TEMPLATE İÇERİSİNDE ÇAĞIRAMIYORUZ, sabit bir veriymiş
    // gibi kullanıyoruz, yukarıda buradaki metodların nasıl kullanıldığına bakın
    computed: {
        currentTemperature() {
            return Math.round(this.currentData.main.temp)
        },
        // Saatlik parçalar halinde gelen verileri JSON nesnelerine map le
        // Map hakkında detaylı bilgi için:
        // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
        mapDailyDataToWeatherInfo() {
            return this.dailyData.list.map((listElement) => {
                let desc = listElement.weather[0].description;
                return {
                    date: listElement.dt_txt,
                    temperature: Math.round(listElement.main.temp),
                    // Gelen açıklama bilgisinin ilk harfini büyük harfe çevir
                    // öbür türlü estetik görünmüyor
                    description: desc.charAt(0).toUpperCase() + desc.slice(1),
                    icon: this.getIcon(listElement.weather[0].icon)
                }
            })
        }
    },
    // Burada tanımladığımız metodları template içerisinde kullanabiliyoruz
    methods: {
        getDate(unix) {
            let data = new Date(unix * 1000);
            return data.toLocaleString();
        },
        // Gelen veriler aynı zaman icon kodlarını da içeriyor, bu kodları kullanarak
        // OpenWeatherMap'ten icon resimlerini çekebiliyoruz
        getIcon(icon) {
            let url = `http://openweathermap.org/img/wn/${icon}@2x.png`
            return url
        }
    },
}
</script>

<style scoped>

</style>