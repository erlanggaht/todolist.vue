<script setup>
import { ref } from 'vue';


const props = defineProps({
    alerts:Object // >>> alerts.boolean
})
const activeClass = ref('alert')
const errorClass = ref('alert_hidden')

</script>


<template>

    <section :class="alerts.boolean ? 'alert' : 'alert_hidden'">
        <figure style="text-align: center;">
            <img src="../assets//check.gif" alt="check" style="transform:scale(1.2)" />
            <figcaption class="success_save">successfully saved the task. Thank You (❁´◡`❁)</figcaption>
        </figure>
    </section>

</template>

<style scoped>

.alert {
    position: absolute;
    background-color: #fdfdfd;
    top:0;bottom: 0;left: 0;right: 0;
    z-index: 999999;
    border-radius: 3rem;
    display: flex;justify-content: center;align-items: center;
    transition: all .7s;
    height: 100%;
    visibility:visible;

}

.alert_hidden {
    height: 0;
    font-size: 0;
    visibility: hidden;
}

.success_save {
    color:#222;font-weight:700;font-size:1.2rem;text-transform:uppercase;
    font-family: 'Roboto Condensed', sans-serif;
    padding: 1rem 0;
    transition: all .7s;

}

</style>