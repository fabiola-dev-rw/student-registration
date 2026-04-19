<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const password = ref('')
const error = ref('')
const loading = ref(false)

const handleLogin = async () => {
  error.value = ''
  loading.value = true

  // Validate form
  if (!email.value || !password.value) {
    error.value = 'Please enter both email and password'
    loading.value = false
    return
  }

  // Simulate admin credentials (hardcoded for demo)
  if (email.value === 'admin@etraining.com' && password.value === 'admin123') {
    localStorage.setItem('adminLoggedIn', 'true')
    localStorage.setItem('adminEmail', email.value)
    router.push('/admin/dashboard')
  } else {
    error.value = 'Invalid email or password. Try admin@etraining.com / admin123'
    loading.value = false
  }
}

const handleBackToHome = () => {
  router.push('/')
}
</script>

<template>
  <div class="login-page">
    <nav class="navbar">
      <div class="nav-container">
        <div class="logo">e-Training Portal</div>
        <div class="back-link" @click="handleBackToHome">← Back to Home</div>
      </div>
    </nav>

    <div class="login-container">
      <div class="login-card">
        <h1>Admin Login</h1>
        <p class="subtitle">Access the admin dashboard to review applications</p>

        <form @submit.prevent="handleLogin" class="login-form">
          <div v-if="error" class="alert alert-error">
            {{ error }}
          </div>

          <div class="form-group">
            <label for="email">Email Address</label>
            <input
              id="email"
              v-model="email"
              type="email"
              placeholder="Enter your email"
              required
            />
          </div>

          <div class="form-group">
            <label for="password">Password</label>
            <input
              id="password"
              v-model="password"
              type="password"
              placeholder="Enter your password"
              required
            />
          </div>

          <button type="submit" class="btn btn-login" :disabled="loading">
            {{ loading ? 'Logging in...' : 'Login' }}
          </button>
        </form>

        <div class="demo-credentials">
          <h3>Demo Credentials</h3>
          <p><strong>Email:</strong> admin@etraining.com</p>
          <p><strong>Password:</strong> admin123</p>
        </div>

        <div class="additional-links">
          <a href="#" @click.prevent="handleBackToHome">← Back to Home</a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.login-page {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Navbar */
.navbar {
  background: rgba(0, 0, 0, 0.1);
  padding: 1rem 0;
  backdrop-filter: blur(10px);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
}

.back-link {
  color: white;
  cursor: pointer;
  text-decoration: none;
  font-weight: 500;
  transition: opacity 0.3s ease;
}

.back-link:hover {
  opacity: 0.8;
}

/* Login Container */
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: calc(100vh - 60px);
  padding: 2rem;
}

.login-card {
  background: white;
  padding: 3rem;
  border-radius: 15px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  width: 100%;
  max-width: 400px;
}

.login-card h1 {
  font-size: 2rem;
  color: #667eea;
  margin-bottom: 0.5rem;
  text-align: center;
}

.subtitle {
  color: #666;
  text-align: center;
  margin-bottom: 2rem;
}

/* Form */
.login-form {
  margin-bottom: 2rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  color: #333;
  font-weight: 600;
}

.form-group input {
  width: 100%;
  padding: 0.75rem;
  border: 2px solid #e0e0e0;
  border-radius: 5px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-group input:focus {
  outline: none;
  border-color: #667eea;
}

.form-group input::placeholder {
  color: #999;
}

/* Alert */
.alert {
  padding: 1rem;
  border-radius: 5px;
  margin-bottom: 1.5rem;
  text-align: center;
}

.alert-error {
  background-color: #ffe0e0;
  color: #d32f2f;
  border: 1px solid #d32f2f;
}

/* Button */
.btn {
  width: 100%;
  padding: 0.75rem;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-login {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.btn-login:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.btn-login:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

/* Demo Credentials */
.demo-credentials {
  background: #f5f5f5;
  padding: 1.5rem;
  border-radius: 8px;
  margin-bottom: 1.5rem;
}

.demo-credentials h3 {
  color: #667eea;
  margin-bottom: 0.75rem;
  font-size: 0.95rem;
}

.demo-credentials p {
  color: #555;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  font-family: 'Courier New', monospace;
}

/* Additional Links */
.additional-links {
  text-align: center;
}

.additional-links a {
  color: #667eea;
  text-decoration: none;
  font-weight: 500;
  transition: opacity 0.3s ease;
}

.additional-links a:hover {
  opacity: 0.8;
}

@media (max-width: 768px) {
  .navbar {
    padding: 0.75rem 0;
  }

  .nav-container {
    padding: 0 1rem;
  }

  .logo {
    font-size: 1.2rem;
  }

  .back-link {
    font-size: 0.9rem;
  }

  .login-container {
    padding: 1rem;
  }

  .login-card {
    padding: 2rem 1.5rem;
    max-width: 100%;
  }

  .login-card h1 {
    font-size: 1.5rem;
  }

  .subtitle {
    font-size: 0.95rem;
  }

  .form-group input {
    font-size: 16px; /* Prevents zoom on iOS */
  }

  .btn-login {
    padding: 0.65rem;
  }

  .demo-credentials {
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .nav-container {
    flex-direction: column;
    gap: 0.5rem;
    padding: 0 1rem;
  }

  .logo {
    font-size: 1rem;
  }

  .back-link {
    font-size: 0.8rem;
  }

  .login-container {
    min-height: calc(100vh - 100px);
    padding: 1rem;
  }

  .login-card {
    padding: 1.5rem;
    border-radius: 10px;
  }

  .login-card h1 {
    font-size: 1.2rem;
  }

  .subtitle {
    font-size: 0.85rem;
  }

  .form-group {
    margin-bottom: 1rem;
  }

  .form-group label {
    font-size: 0.9rem;
  }

  .form-group input {
    padding: 0.65rem;
    font-size: 16px;
  }

  .btn-login {
    padding: 0.6rem;
    font-size: 0.95rem;
  }

  .demo-credentials {
    padding: 1rem;
    font-size: 0.8rem;
  }

  .demo-credentials h3 {
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
  }

  .demo-credentials p {
    margin-bottom: 0.3rem;
  }
}
</style>
