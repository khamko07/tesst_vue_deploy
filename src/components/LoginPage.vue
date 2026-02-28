<template>
  <div class="login-container">
    <div class="login-box">
      <div class="login-header">
        <img alt="Vue logo" src="../assets/logo.png" class="logo" />
        <h2>Đăng Nhập</h2>
        <p>Chào mừng bạn trở lại!</p>
      </div>

      <form @submit.prevent="handleLogin" class="login-form">
        <div class="form-group">
          <label for="username">Tên đăng nhập</label>
          <div class="input-wrapper">
            <span class="icon">👤</span>
            <input
              id="username"
              v-model="form.username"
              type="text"
              placeholder="Nhập tên đăng nhập"
              :class="{ 'input-error': errors.username }"
            />
          </div>
          <span class="error-msg" v-if="errors.username">{{ errors.username }}</span>
        </div>

        <div class="form-group">
          <label for="password">Mật khẩu</label>
          <div class="input-wrapper">
            <span class="icon">🔒</span>
            <input
              id="password"
              v-model="form.password"
              :type="showPassword ? 'text' : 'password'"
              placeholder="Nhập mật khẩu"
              :class="{ 'input-error': errors.password }"
            />
            <span class="toggle-password" @click="showPassword = !showPassword">
              {{ showPassword ? '🙈' : '👁️' }}
            </span>
          </div>
          <span class="error-msg" v-if="errors.password">{{ errors.password }}</span>
        </div>

        <div class="form-options">
          <label class="remember-me">
            <input type="checkbox" v-model="form.remember" />
            <span>Ghi nhớ đăng nhập</span>
          </label>
          <a href="#" class="forgot-password">Quên mật khẩu?</a>
        </div>

        <div class="alert alert-error" v-if="loginError">
          ❌ {{ loginError }}
        </div>

        <div class="alert alert-success" v-if="loginSuccess">
          ✅ Đăng nhập thành công! Chào mừng <strong>{{ form.username }}</strong>!
        </div>

        <button type="submit" class="login-btn" :disabled="isLoading">
          <span v-if="isLoading">⏳ Đang đăng nhập...</span>
          <span v-else>Đăng Nhập</span>
        </button>
      </form>

      <div class="login-footer">
        <p>Chưa có tài khoản? <a href="#">Đăng ký ngay</a></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginPage',
  data() {
    return {
      form: {
        username: '',
        password: '',
        remember: false
      },
      errors: {
        username: '',
        password: ''
      },
      showPassword: false,
      isLoading: false,
      loginError: '',
      loginSuccess: false
    }
  },
  methods: {
    validate() {
      this.errors = { username: '', password: '' }
      let isValid = true

      if (!this.form.username.trim()) {
        this.errors.username = 'Vui lòng nhập tên đăng nhập'
        isValid = false
      }

      if (!this.form.password) {
        this.errors.password = 'Vui lòng nhập mật khẩu'
        isValid = false
      } else if (this.form.password.length < 6) {
        this.errors.password = 'Mật khẩu phải có ít nhất 6 ký tự'
        isValid = false
      }

      return isValid
    },

    async handleLogin() {
      this.loginError = ''
      this.loginSuccess = false

      if (!this.validate()) return

      this.isLoading = true

      // Giả lập gọi API
      await new Promise(resolve => setTimeout(resolve, 1500))

      // Kiểm tra tài khoản demo
      if (this.form.username === 'admin' && this.form.password === '123456') {
        this.loginSuccess = true
      } else {
        this.loginError = 'Tên đăng nhập hoặc mật khẩu không đúng!'
      }

      this.isLoading = false
    }
  }
}
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

.login-box {
  background: white;
  border-radius: 16px;
  padding: 40px;
  width: 100%;
  max-width: 420px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
}

.login-header {
  text-align: center;
  margin-bottom: 30px;
}

.logo {
  width: 80px;
  margin-bottom: 16px;
}

.login-header h2 {
  font-size: 28px;
  color: #333;
  margin-bottom: 8px;
}

.login-header p {
  color: #888;
  font-size: 14px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  color: #555;
  font-weight: 600;
  font-size: 14px;
}

.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.icon {
  position: absolute;
  left: 12px;
  font-size: 16px;
}

.input-wrapper input {
  width: 100%;
  padding: 12px 40px 12px 40px;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 15px;
  transition: border-color 0.3s;
  outline: none;
}

.input-wrapper input:focus {
  border-color: #667eea;
}

.input-error {
  border-color: #e74c3c !important;
}

.toggle-password {
  position: absolute;
  right: 12px;
  cursor: pointer;
  font-size: 16px;
}

.error-msg {
  color: #e74c3c;
  font-size: 12px;
  margin-top: 5px;
  display: block;
}

.form-options {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.remember-me {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  font-size: 14px;
  color: #555;
}

.forgot-password {
  font-size: 14px;
  color: #667eea;
  text-decoration: none;
  font-weight: 600;
}

.forgot-password:hover {
  text-decoration: underline;
}

.alert {
  padding: 12px 16px;
  border-radius: 8px;
  margin-bottom: 16px;
  font-size: 14px;
}

.alert-error {
  background: #ffeaea;
  color: #e74c3c;
  border: 1px solid #f5c6cb;
}

.alert-success {
  background: #eafaf1;
  color: #27ae60;
  border: 1px solid #c3e6cb;
}

.login-btn {
  width: 100%;
  padding: 14px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: opacity 0.3s, transform 0.1s;
}

.login-btn:hover:not(:disabled) {
  opacity: 0.9;
  transform: translateY(-1px);
}

.login-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.login-footer {
  text-align: center;
  margin-top: 24px;
  font-size: 14px;
  color: #888;
}

.login-footer a {
  color: #667eea;
  font-weight: 600;
  text-decoration: none;
}

.login-footer a:hover {
  text-decoration: underline;
}
</style>
