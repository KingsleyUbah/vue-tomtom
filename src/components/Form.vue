<template>
    <div class="form">
        <input type="text"  placeholder="longitude" v-model="longitude">
        <input type="text"  placeholder="latitude" v-model="latitude">
        <button @click="sendLocation">Add Location</button>
    </div>
</template>



<script>
import { ref } from 'vue'

export default {
    setup(props, context) {
        const latitude = ref('')
        const longitude = ref('')
        

        const sendLocation = () => {
            context.emit('useLocation', {lat: Number(latitude.value), lng: Number(longitude.value)})
        }

        return {
            longitude,
            latitude,
            sendLocation
        }       
    },
}
</script>



<style>
    .form {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 3rem 0;
    }

    input {
        padding: .7rem;
        margin-right: .5rem;
        font-size: 1rem;
        border-radius: 5px;
        border: none;
    }

    button {
        font-size: 1rem;
        padding: .9rem;
        background-color: cadetblue;
        border: none;
        border-radius: 5px;
        color: white;
    }
</style>
