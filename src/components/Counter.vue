<script setup>
import { ref, onMounted, defineProps } from 'vue'

const count = ref(0)

defineProps({
    messageText: String,
    changeMessage: Function
})

onMounted(() => {
    console.log('on Mounted at Counter.vue');
})
</script>

<template>
    <div>Hello {{ messageText }}</div>
    <div>
        <input type="text" v-model="message">
        <button @click="changeMessage(message)">
            Change message from counter 
        </button>
    </div>
    <button @click="count++">You cliked me {{ count }} times.</button>
</template>