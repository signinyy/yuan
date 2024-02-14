<template>
  <div class="login-container">
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="username">Username</label>
        <input
            type="text"
            id="username"
            v-model="form.username"
            placeholder="Enter your username"
            required
        />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input
            type="password"
            id="password"
            v-model="form.password"
            placeholder="Enter your password"
            required
        />
      </div>
      <button type="submit" class="login-button">{{ submitButtonText }}</button>
    </form>
    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
  </div>
</template>

<script>
export default {
  name:'UserLogin',
  data() {
    return {
      form: {
        username: '',
        password: ''
      },
      errorMessage: '',
      submitButtonText: '登录 / 注册'
    };
  },
  methods: {
    async handleSubmit() {
      try {
        // 发送请求到后端进行注册或登录
        const response = await this.$http.post('/api/auth', this.form);

        // 根据后端返回的信息处理登录或注册逻辑
        if (response.data.success) {
          // 如果注册成功，可能需要将用户重定向到登录页面或主页
          // 这里只是简单地将提交按钮的文本改为"Login"
          this.submitButtonText = 'Login';
          // 清除表单
          this.form.username = '';
          this.form.password = '';
          this.errorMessage = '';
        } else {
          // 显示错误信息
          this.errorMessage = response.data.message;
        }
      } catch (error) {
        // 处理网络错误或其他错误
        console.error(error);
        this.errorMessage = 'An error occurred.';
      }
    }
  }
};
</script>
<style scoped>
.login-container {
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  background-color: #fff;
  margin-top: 100px;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input {
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ddd;
}

.login-button {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 4px;
  background-color: #4caf50;
  color: white;
  cursor: pointer;
}

.login-button:hover {
  background-color: #45a049;
}
</style>