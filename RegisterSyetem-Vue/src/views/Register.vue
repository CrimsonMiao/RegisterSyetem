<template>
  <div class="register-container">
    <div class="register-content">
      <!-- 左侧内容 -->
      <div class="left-section">
        <div class="background-gradient"></div>
        <h1 class="main-title">Join Us Today</h1>
        <p class="login-text">
          Already have an account? 
          <router-link to="/" class="login-link">Sign in here.</router-link>
        </p>
      </div>

      <!-- 右侧表单 -->
      <div class="right-section">
        <form class="register-form">
          <div class="form-group">
            <label for="fullName">Full Name</label>
            <input 
              type="text" 
              id="fullName" 
              v-model="fullName"
              class="form-input"
              placeholder=""
            />
          </div>

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
                :type="showPassword ? 'text' : 'password'" 
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

          <div class="form-group">
            <label for="confirmPassword">Confirm Password</label>
            <div class="password-input-wrapper">
              <input 
                :type="showConfirmPassword ? 'text' : 'password'" 
                id="confirmPassword" 
                v-model="confirmPassword"
                class="form-input"
                placeholder=""
              />
              <button 
                type="button" 
                class="password-toggle"
                @click="toggleConfirmPasswordVisibility"
              >
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                  <circle cx="12" cy="12" r="3"></circle>
                </svg>
              </button>
            </div>
          </div>

          <div class="terms-checkbox">
            <input 
              type="checkbox" 
              id="terms" 
              v-model="agreeTerms"
              class="checkbox-input"
            />
            <label for="terms" class="checkbox-label">
              I agree to the <a href="#" class="terms-link">Terms of Service</a> and <a href="#" class="terms-link">Privacy Policy</a>
            </label>
          </div>

          <button type="submit" class="register-button" @click.prevent="handleRegister">
            Create Account
          </button>
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
const fullName = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const agreeTerms = ref(false)
const showPassword = ref(false)
const showConfirmPassword = ref(false)

const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value
}

const toggleConfirmPasswordVisibility = () => {
  showConfirmPassword.value = !showConfirmPassword.value
}

const handleRegister = async () => {
  try {
    const response = await axios.post('https://fodkigunmamz.sealosbja.site/api/register', {
      username: fullName.value,
      password: password.value,
    });
    // 注册成功后跳转到登录页面
    if (response.status === 201) {
      router.push('/');
    } else {
      alert('注册失败');
    }
  } catch (error) {
    alert('注册失败');
  }
}
</script>

<style scoped>
.register-container {
  min-height: 100vh;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.register-content {
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

.login-text {
  font-size: 1rem;
  text-align: center;
  position: relative;
  z-index: 1;
  margin: 0;
}

.login-link {
  color: #3b82f6;
  text-decoration: none;
  font-weight: 500;
}

.login-link:hover {
  text-decoration: underline;
}

.right-section {
  flex: 1;
  padding: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.register-form {
  width: 100%;
  max-width: 400px;
}

.form-group {
  margin-bottom: 16px;
}

.form-group label {
  display: block;
  margin-bottom: 6px;
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

.terms-checkbox {
  display: flex;
  align-items: flex-start;
  margin-bottom: 24px;
  gap: 8px;
}

.checkbox-input {
  margin: 0;
  margin-top: 2px;
}

.checkbox-label {
  font-size: 0.9rem;
  color: #6b7280;
  line-height: 1.4;
  margin: 0;
  cursor: pointer;
}

.terms-link {
  color: #3b82f6;
  text-decoration: none;
}

.terms-link:hover {
  text-decoration: underline;
}

.register-button {
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
}

.register-button:hover {
  background-color: #2563eb;
}

@media (max-width: 768px) {
  .register-content {
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
