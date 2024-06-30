<template>
  <div>
    <form @submit.prevent="handleLogin" class="form-container">
      <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p><br>
      <div class="form-group">
        <label for="email" class="form-label">Your email</label>
        <input 
          type="email" 
          id="email" 
          class="form-input"
          v-model="email" 
          required 
        />
      </div>
      <div class="form-group">
        <label for="password" class="form-label">Your password</label>
        <input 
          type="password" 
          id="password" 
          class="form-input" 
          v-model="password" 
          required 
        />
      </div>
      <button type="submit" class="form-button">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      errorMessage: ''
    };
  },
  methods: {
    async handleLogin() {
      try {
        // Simulação de autenticação. Substitua por uma chamada real ao seu backend
        if (this.email === 'test@example.com' && this.password === 'password') {
          // Armazenar token no localStorage (ou em cookies)
          localStorage.setItem('authToken', 'fakeToken');
          
          // Redirecionar para a página principal
          this.$router.push('/');
        } else {
          this.errorMessage = 'Credenciais inválidas';
        }
      } catch (error) {
        this.errorMessage = 'Erro ao tentar fazer login';
      }
    }
  }
};
</script>

<style>
.error-message{
  background-color: red;
  color: white;
  padding: 15px;
  border-radius: 10px;
  font-size: 20px;
}

.form-container {
      max-width: 28rem;
      margin: auto;
      background-color: #fff;
      border-radius: 0.5rem;
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
      font-family: sans-serif;
      margin-top: 150px;

    }
    .form-group {
      margin-bottom: 1.25rem;
    }
    .form-label {
      display: block;
      margin-bottom: 0.5rem;
      font-size: 0.875rem;
      font-weight: 500;
      color: #1f2937;
    }
    .form-input {
      width: 100%;
      padding: 0.625rem;
      font-size: 0.875rem;
      border: 1px solid #d1d5db;
      border-radius: 0.5rem;
      background-color: #f9fafb;
      color: #374151;
      transition: border-color 0.3s, box-shadow 0.3s;
    }
    .form-input:focus {
      border-color: #3b82f6;
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.5);
      outline: none;
    }
    .form-checkbox {
      width: 1rem;
      height: 1rem;
      border: 1px solid #d1d5db;
      border-radius: 0.25rem;
      background-color: #f9fafb;
      color: #374151;
      transition: border-color 0.3s, box-shadow 0.3s;
    }
    .form-checkbox:focus {
      border-color: #3b82f6;
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.5);
      outline: none;
    }
    .form-checkbox-label {
      margin-left: 0.5rem;
      font-size: 0.875rem;
      font-weight: 500;
      color: #1f2937;
    }
    .form-button {
      display: inline-block;
      width: 100%;
      padding: 0.625rem 1.25rem;
      font-size: 0.875rem;
      font-weight: 500;
      color: #fff;
      background-color: #3b82f6;
      border: none;
      border-radius: 0.5rem;
      cursor: pointer;
      transition: background-color 0.3s, box-shadow 0.3s;
    }
    .form-button:hover {
      background-color: #2563eb;
    }
    .form-button:focus {
      box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.5);
      outline: none;
    }
</style>