<script setup>
import { ref, reactive, watch } from 'vue'

const fromData = reactive({
    firstname: '',
    lastname: ''
})
const fullname = ref('')

watch(
    () => [fromData.firstname, fromData.lastname],
    (newFullname, oldFullname) => {
        fullname.value = `${newFullname[0]} ${newFullname[1]}`
    }
)
</script>

<template>
    <div>
        <div>Fallname: {{ fullname }}</div>
        <input type="text" v-model="fromData.firstname">
        <input type="text" v-model="fromData.lastname">
    </div>
</template>