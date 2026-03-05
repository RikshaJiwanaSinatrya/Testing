<script setup>
import { reactive, ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const form = reactive({
  email: '',
  password: '',
})
const error = ref('')

const submitLogin = () => {
  const email = form.email.trim()
  const password = form.password.trim()

  if (!email || !password) {
    error.value = 'Email dan password wajib diisi.'
    return
  }

  localStorage.setItem('userRole', 'admin')
  localStorage.setItem('isLoggedIn', 'true')
  error.value = ''
  router.push('/dashboard')
}

const continueAsCustomer = () => {
  localStorage.setItem('userRole', 'customer')
  localStorage.removeItem('isLoggedIn')
  error.value = ''
  router.push('/order')
}
</script>

<template>
  <section class="login-page">
  <div class="login-wrapper">
    <form class="login-card" @submit.prevent="submitLogin">
      <h1>Login Admin</h1>
      <p class="subtitle">Masuk sebagai admin atau lewati untuk lanjut sebagai pelanggan.</p>

      <label for="email">Email</label>
      <input id="email" v-model="form.email" type="email" placeholder="username@example.com" />

      <label for="password">Password</label>
      <input id="password" v-model="form.password" type="password" placeholder="Masukkan password" />

      <p v-if="error" class="error-text">{{ error }}</p>

      <button type="submit">Masuk sebagai Admin</button>
      <button type="button" class="btn-skip" @click="continueAsCustomer">
        Lewati, lanjut sebagai pelanggan
      </button>
    </form>
  </div>
  </section>
</template>

<style scoped>
.login-page {
  min-height: 100vh;
  display: grid;
  place-items: start;
  background: radial-gradient(circle at top, #1f2937 0%, #0f172a 55%, #020617 100%);
}

.login-wrapper {
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: flex-start;
}

.login-card {
  width: 100%;
  max-width: 900px;
  min-height: 100vh;
  padding: 40px 200px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: #23374b;
  box-shadow: 0 20px 40px rgba(2, 6, 23, 0.45);
  border-radius: 0 18px 18px 0;
  gap: 10px;
}

.login-card h1 {
  margin: 0;
  font-size: 28px;
  color: #cdcdcd;
  text-align: center;
}

.login-card .subtitle {
  margin: 0 0 18px;
  color: #5b708f;
  text-align: center;
}

.login-card label {
  font-size: 13px;
  font-weight: 600;
  color: #5b708f;
}

.login-card input {
  width: 100%;
  border: 1px solid #5b708f;
  border-radius: 10px;
  padding: 11px 12px;
  font-size: 14px;
  color: #cdcdcd;
  background-color: #26405a;
  transition: border-color 0.2s ease, box-shadow 0.2s ease, background-color 0.2s ease;
}

.login-card input:focus {
  background-color: #26405a;
  outline: none;
  box-shadow: 0 0 0 3px rgba(0, 78, 161, 0.28);
  border-color: #004ea1;
  color: #cdcdcd;
}

.login-card input::placeholder {
  color: #8ca0bc;
}

.login-card input:-webkit-autofill,
.login-card input:-webkit-autofill:hover,
.login-card input:-webkit-autofill:focus,
.login-card input:-webkit-autofill:active {
  -webkit-text-fill-color: #cdcdcd;
  -webkit-box-shadow: 0 0 0 1000px #26405a inset;
  box-shadow: 0 0 0 1000px #26405a inset;
  caret-color: #cdcdcd;
  transition: background-color 5000s ease-in-out 0s;
}

.error-text {
  margin: 4px 0;
  color: #dc2626;
  font-size: 13px;
}

.login-card button {
  margin-top: 8px;
  border: 0;
  border-radius: 10px;
  padding: 12px;
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  background: #16a34a;
  color: #ecfdf5;
}

.login-card button:hover {
  background: #15803d;
}

.login-card .btn-skip {
  margin-top: 4px;
  background: #0f172a;
  color: #f8fafc;
}

.login-card .btn-skip:hover {
  background: #1e293b;
}
</style>
