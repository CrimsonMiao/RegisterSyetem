<template>
  <div class="home-container">
    <div class="home-content">
      <h1 class="welcome-title">欢迎来到主页,{{ userName }}</h1>
      <p class="welcome-subtitle">您已成功登录系统</p>
      <button @click="logout" class="logout-button">退出登录</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const userName = ref('')
const userId = ref(localStorage.getItem('userId'))

if (!userId.value) {
  router.push('/')
}

const getUserInfo = async () => {
  try {
    const { data } = await axios.get(`https://fodkigunmamz.sealosbja.site/api/user/${userId.value}`)
    userName.value = data.data.username
    // console.log(userName.value) // 如无调试需求可移除
  } catch (error) {
    console.error('获取用户信息失败:', error)
    // 可根据需求添加错误处理逻辑
  }
}

onMounted(() => {
  getUserInfo()
})

const logout = () => {
  localStorage.removeItem('userId')
  router.push('/')
}
</script>

<style scoped>
.home-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.home-content {
  text-align: center;
  color: white;
  padding: 60px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  backdrop-filter: blur(10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.welcome-title {
  font-size: 3rem;
  font-weight: 700;
  margin: 0 0 20px 0;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.welcome-subtitle {
  font-size: 1.2rem;
  margin: 0 0 40px 0;
  opacity: 0.9;
}

.logout-button {
  background-color: rgba(255, 255, 255, 0.2);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  padding: 12px 24px;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
  backdrop-filter: blur(10px);
}

.logout-button:hover {
  background-color: rgba(255, 255, 255, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

@media (max-width: 768px) {
  .home-content {
    padding: 40px 20px;
    margin: 20px;
  }
  
  .welcome-title {
    font-size: 2rem;
  }
  
  .welcome-subtitle {
    font-size: 1rem;
  }
}
</style>
