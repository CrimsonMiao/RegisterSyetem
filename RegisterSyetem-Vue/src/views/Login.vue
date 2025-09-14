<template>
  <div class="login-container">
    <div class="login-content">
      <!-- 左侧内容 -->
      <div class="left-section">
        <div class="background-gradient"></div>
        <h1 class="main-title">Sign In to Open the World</h1>
        <p class="register-text">
          If you don't have an account, you can 
          <router-link to="/register" class="register-link">Register here.</router-link>
        </p>
      </div>

      <!-- 右侧表单 -->
      <div class="right-section">
        <form class="login-form">
          <div class="form-group">
            <label for="email">Your email address</label>
            <input 
              type="email" 
              id="email" 
              v-model="email"
              class="form-input"
              placeholder=""
            />
          </div>

          <div class="form-group">
            <label for="password">Password</label>
            <div class="password-input-wrapper">
              <input 
                type="password" 
                id="password" 
                v-model="password"
                class="form-input"
                placeholder=""
              />
              <button 
                type="button" 
                class="password-toggle"
                @click="togglePasswordVisibility"
              >
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                  <circle cx="12" cy="12" r="3"></circle>
                </svg>
              </button>
            </div>
          </div>

          <a href="#" class="recovery-link">Recovery password</a>

          <button type="submit" class="signin-button" @click.prevent="handleLogin">
            Sign In
          </button>

          <div class="divider">
            <span>or continue with</span>
          </div>

          <div class="social-login">
            <button type="button" class="social-button google">
              <svg width="20" height="20" viewBox="0 0 24 24">
                <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
              </svg>
            </button>
            <button type="button" class="social-button apple">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.78 17.09 3 13.52 3 9.73 3 5.96 5.38 3.5 8.1 3.5c1.64 0 3.08.99 3.97.99.89 0 2.4-1.01 4.03-.99 1.14.01 2.19.5 2.91 1.24-2.18 1.33-1.81 5.99.33 6.7.91.3 1.68.13 2.33-.09.19-.07.4-.15.6-.22-.15.46-.34.9-.56 1.32zM13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/>
              </svg>
            </button>
            <button type="button" class="social-button facebook">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="#1877F2">
                <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
              </svg>
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const email = ref('')
const password = ref('')
const showPassword = ref(false)

const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value
  const passwordInput = document.getElementById('password')
  if (passwordInput) {
    passwordInput.type = showPassword.value ? 'text' : 'password'
  }
}

const handleLogin = async () => {
  // 简单的登录逻辑，这里可以添加实际的登录验证
  try {
    const response = await axios.post('https://fodkigunmamz.sealosbja.site/api/login', {
      username: email.value,
      password: password.value,
    });
    if (response.status === 200) {
      localStorage.setItem('userId', response.data.data.userId)
      router.push('/home')
    } else {
      alert('登录失败');
    }
  } catch (error) {
    alert('登录失败');
  }

}
</script>

<style scoped>
.login-container {
  min-height: 100vh;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.login-content {
  display: flex;
  width: 100%;
  max-width: 1200px;
  height: 600px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
  overflow: hidden;
}

.left-section {
  flex: 1;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 60px;
  color: white;
}

.background-gradient {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  filter: blur(20px);
  opacity: 0.7;
}

.main-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 0 0 20px 0;
  text-align: center;
  position: relative;
  z-index: 1;
}

.register-text {
  font-size: 1rem;
  text-align: center;
  position: relative;
  z-index: 1;
  margin: 0;
}

.register-link {
  color: #3b82f6;
  text-decoration: none;
  font-weight: 500;
}

.register-link:hover {
  text-decoration: underline;
}

.right-section {
  flex: 1;
  padding: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.login-form {
  width: 100%;
  max-width: 400px;
}

.form-group {
  margin-bottom: 24px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  color: #374151;
  font-size: 0.9rem;
}

.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.2s;
  box-sizing: border-box;
}

.form-input:focus {
  outline: none;
  border-color: #3b82f6;
}

.password-input-wrapper {
  position: relative;
}

.password-toggle {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
  color: #6b7280;
  padding: 4px;
}

.password-toggle:hover {
  color: #374151;
}

.recovery-link {
  display: block;
  text-align: left;
  color: #6b7280;
  text-decoration: none;
  font-size: 0.9rem;
  margin-bottom: 24px;
}

.recovery-link:hover {
  color: #374151;
  text-decoration: underline;
}

.signin-button {
  width: 100%;
  background-color: #3b82f6;
  color: white;
  border: none;
  padding: 14px;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s;
  box-shadow: 0 4px 6px rgba(59, 130, 246, 0.3);
  margin-bottom: 24px;
}

.signin-button:hover {
  background-color: #2563eb;
}

.divider {
  position: relative;
  text-align: center;
  margin: 24px 0;
  color: #6b7280;
  font-size: 0.9rem;
}

.divider::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  height: 1px;
  background-color: #e5e7eb;
}

.divider span {
  background-color: white;
  padding: 0 16px;
  position: relative;
  z-index: 1;
}

.social-login {
  display: flex;
  gap: 12px;
  justify-content: center;
}

.social-button {
  width: 48px;
  height: 48px;
  border: 2px solid #e5e7eb;
  background-color: white;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
}

.social-button:hover {
  border-color: #d1d5db;
  background-color: #f9fafb;
}

.social-button svg {
  display: block;
}

@media (max-width: 768px) {
  .login-content {
    flex-direction: column;
    height: auto;
    margin: 20px;
  }
  
  .left-section {
    padding: 40px 20px;
  }
  
  .right-section {
    padding: 40px 20px;
  }
  
  .main-title {
    font-size: 2rem;
  }
}
</style>
