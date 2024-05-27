<script setup>
import { ref, computed, onMounted, watch } from 'vue'

const isLoading = ref(false)
const isUpdated = ref(false)
const isValid = ref(true)

const firstname = ref('')
const lastname = ref('')
const email = ref('')
const errors = ref({})

const fullname = computed(() => {
  return `${firstname.value} ${lastname.value}`
})

const updateProfile = async () => {
  isLoading.value = true
  // จำลองการส่ง API
  await (new Promise(resolve => setTimeout(resolve, 2000)))
  isLoading.value = false
  isUpdated.value = true
}

const valideteName = (name) => {
  const re = /\d/
  return !re.test(name)
}

const valideteEmail = (eamil) => {
  return email.includes('@')
}

watch([firstname, lastname, email], () => {
  isValid.value = true
  isUpdated.value = false
  errors.value = {}

  if (!valideteName(firstname.value)) {
    isValid.value = false
    errors.value.firstname = 'ชื่อจริงไม่ถูกต้อง'
  }
  
  if (!valideteName(lastname.value)) {
    isValid.value = false
    errors.value.lastname = 'นานสกุลไม่ถูกต้อง'
  }

  if (!valideteEmail(email.value)) {
    isValid.value = false
    errors.value.eamil = 'อีเมลไม่ถูกต้อง'
  }
})

onMounted(() => {
  firstname.value = 'test'
  lastname.value = 'นานสกุล'
  email.value = 'test@mail.com'
})


</script>

<template>
  <div class="container">

    <div>
      <div>Fullname: {{ fullname }}</div>
      <div>email: {{ email }}</div>
    </div>

    <div>
      <div>Firstname</div>
      <input type="text" v-model="firstname">
      <div>{{ errors.firstname }}</div>
    </div>
    <div>
      <div>Lastname</div>
      <input type="text" v-model="lastname">
      <div>{{ errors.lastname }}</div>
    </div>
    <div>
      <div>Email</div>
      <input type="text" v-model="email">
      <div>{{ errors.eamil }}</div>
    </div>

    <div v-if="isLoading" class="loading">Loading...</div>

    <button :disabled="!isValid" class="button" @click="updateProfile()">Update profile</button>

    <div v-if="isUpdated">Profile updated เรียบร้อย</div>
  </div>
</template>

<style>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  max-width: 320px;
  margin: 0 auto;
  flex-direction: column;
}

.container > div {
  width: 100%;
}

input {
  width: 100%;
}

.loading {
  background-color: aliceblue;
  width: 100%;
  padding: 24px;
  box-sizing: border-box;
  margin: 10px 0;
}

.button {
  width: 100%;
  height: 50px;
  margin: 20px;
}
</style>