<template>
  <div class="container">
    <h1>🔐 Connexion</h1>

    <div v-if="error" class="error">{{ error }}</div>
    <div v-if="success" class="success">{{ success }}</div>

    <form @submit.prevent="handleLogin">
      <div class="form-group">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          v-model="form.email"
          placeholder="jean.dupont@example.com"
          required
        />
      </div>

      <div class="form-group">
        <label for="password">Mot de passe</label>
        <input
          type="password"
          id="password"
          v-model="form.password"
          placeholder="Votre mot de passe"
          required
        />
      </div>

      <button type="submit" :disabled="loading">
        {{ loading ? 'Connexion...' : 'Se connecter' }}
      </button>
    </form>

    <div class="link">
      Pas encore de compte ? <router-link to="/register">S'inscrire</router-link>
    </div>

    <div class="divider">
      <span>OU</span>
    </div>

  <button @click="signInWithGoogle" type="button" class="google-btn">
      <svg class="google-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
        <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
        <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
        <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
      </svg>
      Se connecter avec Google
    </button>

    <button @click="signInWithGithub" type="button" class="github-btn">
      <svg class="github-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <path fill="currentColor" d="M12 0C5.37 0 0 5.46 0 12.2c0 5.39 3.44 9.96 8.21 11.58.6.11.82-.27.82-.6 0-.3-.01-1.1-.02-2.16-3.34.74-4.04-1.64-4.04-1.64-.55-1.42-1.34-1.8-1.34-1.8-1.1-.77.08-.76.08-.76 1.22.09 1.86 1.28 1.86 1.28 1.08 1.88 2.83 1.34 3.52 1.02.11-.8.42-1.34.76-1.65-2.66-.31-5.47-1.36-5.47-6.06 0-1.34.46-2.44 1.22-3.3-.12-.31-.53-1.58.12-3.29 0 0 1.01-.33 3.3 1.26a11.1 11.1 0 0 1 6 0c2.28-1.59 3.29-1.26 3.29-1.26.66 1.71.25 2.98.12 3.29.76.86 1.22 1.96 1.22 3.3 0 4.71-2.81 5.75-5.49 6.05.43.38.82 1.1.82 2.22 0 1.61-.01 2.91-.01 3.3 0 .33.22.72.83.6A12.01 12.01 0 0 0 24 12.2C24 5.46 18.63 0 12 0Z"/>
      </svg>
      Se connecter avec GitHub
    </button>

    <button @click="signInWithDiscord" type="button" class="discord-btn">
      <svg class="discord-icon" viewBox="0 0 245 240" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <path fill="currentColor" d="M104.4 104.8c-5.7 0-10.2 5-10.2 11.1 0 6.1 4.6 11.1 10.2 11.1 5.7 0 10.2-5 10.2-11.1.1-6.2-4.5-11.1-10.2-11.1zm36.2 0c-5.7 0-10.2 5-10.2 11.1 0 6.1 4.6 11.1 10.2 11.1 5.7 0 10.2-5 10.2-11.1 0-6.2-4.5-11.1-10.2-11.1z"/>
        <path fill="currentColor" d="M189.5 20h-134C44.2 20 35 29.2 35 40.6v135.2c0 11.4 9.2 20.6 20.5 20.6h113.4l-5.3-18.6 12.8 11.9 12.1 11.1 21.5 19V40.6c0-11.4-9.2-20.6-20.5-20.6zm-38.6 131s-3.6-4.3-6.6-8.1c13.1-3.7 18.1-11.9 18.1-11.9-4.1 2.7-8 4.6-11.5 5.9-5 2.1-9.8 3.4-14.5 4.2-9.6 1.8-18.4 1.3-25.9-.1-5.7-1.1-10.6-2.6-14.7-4.2-2.3-.9-4.8-2-7.3-3.4-.3-.2-.6-.3-.9-.5-.2-.1-.3-.2-.4-.3-1.8-1-2.8-1.7-2.8-1.7s4.8 8 17.5 11.8c-3 3.8-6.7 8.3-6.7 8.3-22.1-.7-30.5-15.1-30.5-15.1 0-32 14.3-58 14.3-58 14.3-10.8 27.9-10.5 27.9-10.5l1 1.2c-17.9 5.1-26.2 13-26.2 13s2.2-1.2 5.9-2.9c10.7-4.7 19.1-6 22.6-6.3.6-.1 1.1-.2 1.7-.2 6.1-.8 13-1 20.2-.2 9.5 1.1 19.7 3.9 30.1 9.6 0 0-7.9-7.5-24.9-12.6l1.4-1.6s13.7-.3 27.9 10.5c0 0 14.3 26 14.3 58 0 .1-8.4 14.5-30.5 15.2z"/>
      </svg>
      Se connecter avec Discord
    </button>

    <div class="jwt-info">
      <h3>💡 Démo JWT</h3>
      <p>
        ✅ Après connexion, un <strong>Access Token</strong> JWT est stocké<br>
        ✅ Ce token est envoyé dans le header <code>Authorization: Bearer ...</code><br>
        ✅ Le serveur vérifie le token sans consulter de session
      </p>
    </div>
  </div>
</template>

<script>
import { authService } from '../services/api'

export default {
  name: 'Login',
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      error: null,
      success: null,
      loading: false
    }
  },
  mounted() {
    // Afficher un message d'erreur si OAuth a échoué
    const error = this.$route.query.error
    if (error === 'google_auth_failed') {
      this.error = 'Échec de l\'authentification Google'
    } else if (error === 'token_generation_failed') {
      this.error = 'Erreur lors de la génération du token'
    }
  },
  methods: {
    async handleLogin() {
      this.error = null
      this.success = null
      this.loading = true

      try {
        const response = await authService.login(this.form)
        this.success = response.message

        // Rediriger vers home après connexion réussie
        setTimeout(() => {
          this.$router.push('/home')
        }, 1000)
      } catch (err) {
        this.error = err.response?.data?.message || 'Erreur lors de la connexion'
      } finally {
        this.loading = false
      }
    },
    signInWithGoogle() {
      // Redirection vers le backend qui initie OAuth
      window.location.href = `${import.meta.env.VITE_API_URL}/auth/google`
    },
    signInWithGithub() {
      window.location.href = `${import.meta.env.VITE_API_URL}/auth/github`
    },
    signInWithDiscord() {
      window.location.href = `${import.meta.env.VITE_API_URL}/auth/discord`
    }
  }
}
</script>

<style scoped>
.divider {
  display: flex;
  align-items: center;
  text-align: center;
  margin: 2rem 0;
  color: #666;
}

.divider::before,
.divider::after {
  content: '';
  flex: 1;
  border-bottom: 1px solid #ddd;
}

.divider span {
  padding: 0 1rem;
  font-size: 0.9rem;
  font-weight: 500;
}

.google-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  background: white;
  color: #3c4043;
  border: 1px solid #dadce0;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.github-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  background: #111827;
  color: #f9fafb;
  border: 1px solid #0f172a;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  margin-top: 0.75rem;
}

.github-btn:hover {
  background: #0b1220;
  border-color: #0b1220;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

.github-icon {
  width: 20px;
  height: 20px;
}

.discord-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  background: #5865F2;
  color: #f9fafb;
  border: 1px solid #4c56d4;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  margin-top: 0.75rem;
}

.discord-btn:hover {
  background: #4b57d8;
  border-color: #4b57d8;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

.discord-icon {
  width: 20px;
  height: 20px;
}

.google-btn:hover {
  background: #f8f9fa;
  border-color: #d2d4d6;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.google-icon {
  width: 20px;
  height: 20px;
}

.jwt-info {
  margin-top: 2rem;
  padding: 1.5rem;
  background: #f0f7ff;
  border-left: 4px solid #2563eb;
  border-radius: 4px;
}

.jwt-info h3 {
  margin: 0 0 0.75rem 0;
  color: #1e40af;
  font-size: 1.1rem;
}

.jwt-info p {
  margin: 0;
  color: #1e3a8a;
  line-height: 1.6;
  font-size: 0.95rem;
}
</style>
