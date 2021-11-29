<template>
    <div>
        <Form @useLocation="useLocation" />
        <div ref="mapRef" class="map"></div>
    </div>
</template>

<script>
import Form from './Form.vue'
import { onMounted, reactive, ref } from 'vue'

export default {
    components: {
        Form
    },

    setup() {
        const mapRef = ref(null)

        const state = reactive({
            locations: [
                { lat: 6.4434, lng: 3.3553 },
                { lat: 6.4442, lng: 3.3561 },
                { lat: 6.4451, lng: 3.3573 },
                { lat: 6.4459, lng: 3.3520 }
            ]
        })

        const useLocation = (location) => {
            state.locations.push(location)
            const lastLocation = state.locations[state.locations.length - 1]

            const tete = window.tt;
            new tete.Marker().setLngLat(lastLocation).addTo(window.map) 
        }

        const insertLocs = (map) => {
            const tomtom = window.tt;

            state.locations.forEach(function (location) {
                var marker = new tomtom.Marker().setLngLat(location).addTo(map) 
                const popup = new tt.Popup({ anchor: 'top' }).setText('UBA Bank')
                marker.setPopup(popup).togglePopup()               
            })
        }


        onMounted(() => {
            const tt = window.tt;

            const focus = { lat: 6.4434, lng: 3.3553 }

            var map = tt.map({
                key: 'Ka5JcBchkVsJSr3gxVgHPC1NcvPO90lG',
                container: mapRef.value,
                center: focus,
                zoom: 15
            })

            map.addControl(new tt.FullscreenControl()); 
            map.addControl(new tt.NavigationControl()); 

            window.map = map

            insertLocs(map)
        })
         

        return {
            useLocation,
            mapRef
        }
    },
}
</script>

<style>
    .map {
        margin: 0 auto;
        height: 70vh;
        width: 50vw;
        background-color: aquamarine;
    }

</style>