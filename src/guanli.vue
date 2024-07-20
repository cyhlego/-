<template>
  <div class="login-container">
    <h2>管理端登录</h2>
    <form @submit.prevent="login">
      <div class="form-group">
        <label for="username">用户名:</label>
        <input type="text" id="username" v-model="username" required>
      </div>
      <div class="form-group">
        <label for="password">密码:</label>
        <input type="password" id="password" v-model="password" required>
      </div>
      <button type="submit">登录</button>
    </form>
    <p v-if="loginError" class="error-message">{{ loginError }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      loginError: ''
    };
  },
  methods: {
    async login() {
      try {
        // 假设这里是发送登录请求的代码，使用axios或者fetch发送POST请求给后端验证
        // 假设登录接口为 /api/login
        const response = await fetch('/api/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            username: this.username,
            password: this.password
          })
        });

        if (response.ok) {
          // 登录成功的操作，可以跳转到管理页面或者设置登录状态等
          alert('登录成功！');
          // 这里可以使用路由进行页面跳转
          // this.$router.push('/dashboard');
        } else {
          // 处理登录失败的情况
          const errorData = await response.json();
          this.loginError = errorData.message || '登录失败，请重试。';
        }
      } catch (error) {
        console.error('登录失败:', error);
        this.loginError = '登录失败，请检查网络连接。';
      }
    }
  }
};
</script>

<style scoped>
.login-container {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.error-message {
  color: red;
  font-size: 14px;
  margin-top: 10px;
}
</style>