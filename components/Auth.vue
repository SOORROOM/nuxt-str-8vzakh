<template>
  <form class="row flex-center flex" @submit.prevent="handleLogin">
    <div class="col-6 form-widget">
      <div class="text-h3">Supabase + Nuxt 3</div>
      <div class="text-body-1">Sign in via magic link with your email below</div>
      <div>
        <v-text-field label="Your email" variant="outlined" v-model="email" placeholder="johndoe@gmail.com"
  type="email"></v-text-field>

      </div>
      <div>
        <v-btn variant="outlined" color="primary"
        :value="loading ? 'Loading' : 'Send magic link'" :disabled="loading"></v-btn>
        
      </div>
    </div>
  </form>
</template>

<script setup>
  const supabase = useSupabaseClient()

  const loading = ref(false)
  const email = ref('')
  const handleLogin = async () => {
    try {
      loading.value = true
      const { error } = await supabase.auth.signInWithOtp({ email: email.value })
      if (error) throw error
      alert('Check your email for the login link!')
    } catch (error) {
      alert(error.error_description || error.message)
    } finally {
      loading.value = false
    }
  }
</script>