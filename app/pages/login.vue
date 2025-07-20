<template>
  <div class="login-container">
    <div class="login-card">
      <!-- 左側圖片區域 -->
      <div class="left-section">
        <div class="image-placeholder">
        </div>
      </div>

      <!-- 右側登入表單 -->
      <div class="right-section">
        <div class="login-form">
          <h2 class="form-title">Login</h2>
          <p class="form-subtitle">Welcome back! Please enter your details.</p>
          
          <div class="form-group">
            <label for="email">Email</label>
            <input 
              id="email"
              v-model="username" 
              type="email"
              placeholder="name@example.com" 
              class="form-input"
            />
          </div>
          
          <div class="form-group">
            <label for="password">Password</label>
            <input 
              id="password"
              v-model="password" 
              type="password"
              placeholder="Password" 
              class="form-input"
            />
            <a href="#" class="forgot-password">Forgot password?</a>
          </div>
          
          <div class="form-group">
            <label class="checkbox-container">
              <input type="checkbox" v-model="rememberMe">
              <span class="checkmark"></span>
              Remember me
            </label>
          </div>
          
          <button @click="login" class="login-button">Sign in</button>
          
          <p class="signup-text">
            Don't have an account? <a href="#" class="signup-link">Sign up</a>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'login',
})

import { ref } from 'vue'
import { useRouter } from 'vue-router'

const username = ref('')
const password = ref('')
const rememberMe = ref(false)
const router = useRouter()

const login = () => {
  if (username.value === 'admin' && password.value === '1234') {
    router.push('/dashboard')
  } else {
    alert('帳號密碼錯誤')
  }
}
</script>

<style scoped>
.login-container {
  display: flex;
  height: 100vh;
  width: 100vw;
  align-items: center;
  justify-content: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  margin: 0;
  padding: 40px;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%); /* 漸層背景 */
  box-sizing: border-box;
}

.login-card {
  display: flex;
  width: 100%;
  max-width: 900px;
  height: 600px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

/* 左側圖片區域 */
.left-section {
  width: 50%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0px;
  position: relative;
  background-image: url('/assets/login.png');
  background-size: cover;
  background-position: center;
}

.image-placeholder {
  width: 100px;
  height: 100;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 32px;
}

.welcome-title {
  color: white;
  font-size: 2.2rem;
  font-weight: 700;
  text-align: center;
  margin: 0;
}

/* 右側登入表單 */
.right-section {
  width: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px;
  background: white;
}

.login-form {
  width: 100%;
  max-width: 400px;
}

.form-title {
  font-size: 2rem;
  font-weight: 600;
  color: #1a202c;
  margin-bottom: 8px;
}

.form-subtitle {
  color: #718096;
  margin-bottom: 32px;
  font-size: 0.95rem;
}

.form-group {
  margin-bottom: 24px;
  position: relative;
}

label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
  margin-bottom: 6px;
}

.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 0.95rem;
  transition: border-color 0.2s, box-shadow 0.2s;
  background: white;
}

.form-input:focus {
  outline: none;
  border-color: #4f46e5;
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
}

.forgot-password {
  position: absolute;
  right: 0;
  top: -28px;
  font-size: 0.875rem;
  color: #4f46e5;
  text-decoration: none;
}

.forgot-password:hover {
  text-decoration: underline;
}

/* 自定義 checkbox */
.checkbox-container {
  display: flex;
  align-items: center;
  cursor: pointer;
  font-size: 0.875rem;
  color: #374151;
}

.checkbox-container input[type="checkbox"] {
  margin-right: 8px;
  width: 16px;
  height: 16px;
}

.login-button {
  width: 100%;
  padding: 12px;
  background: #4f46e5;
  color: white;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.95rem;
  transition: background-color 0.2s;
}

.login-button:hover {
  background: #4338ca;
}

.signup-text {
  text-align: center;
  margin-top: 24px;
  color: #718096;
  font-size: 0.875rem;
}

.signup-link {
  color: #4f46e5;
  text-decoration: none;
  font-weight: 500;
}

.signup-link:hover {
  text-decoration: underline;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .login-container {
    padding: 10px;
    height: auto;
  }
  
  .login-card {
    flex-direction: column;
    height: auto;
    max-width: 400px;
    width: 100%;
  }
  
  .left-section {
    width: 100%;
    padding: 20px;
    min-height: 200px;
    order: 1;
  }

  .right-section {
    width: 100%;
    padding: 20px;
    order: 2;
  }

  .welcome-title {
    font-size: 1.6rem;
    margin-top: 10px;
  }

  .image-placeholder {
    width: 140px;
    height: 140px;
    margin-bottom: 15px;
  }

  .welcome-image {
    max-width: 100%;
    max-height: 100%;
    margin-top: 0;
  }

  .form-title {
    font-size: 1.6rem;
  }

  .form-subtitle {
    font-size: 0.9rem;
    margin-bottom: 20px;
  }

  .login-form {
    max-width: 100%;
  }
}

</style>