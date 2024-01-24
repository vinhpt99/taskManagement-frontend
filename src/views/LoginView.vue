<script setup>
import axios from '@/common/axios-instance';
import { useRouter } from 'vue-router'
import { reactive, ref } from 'vue'
import { mdiAccount, mdiAsterisk } from '@mdi/js'
import SectionFullScreen from '@/components/SectionFullScreen.vue'
import CardBox from '@/components/CardBox.vue'
import FormCheckRadio from '@/components/FormCheckRadio.vue'
import FormField from '@/components/FormField.vue'
import FormControl from '@/components/FormControl.vue'
import BaseButton from '@/components/BaseButton.vue'
import BaseButtons from '@/components/BaseButtons.vue'
import LayoutGuest from '@/layouts/LayoutGuest.vue'
import Loading from '@/components/Loading.vue';
import { useMainStore } from '@/stores/main.js'

const form = reactive({
  login: null,
  pass: null,
  remember: null,
})

const isLoading = ref(false);
const router = useRouter()

const submit = () => {
  isLoading.value = true
  axios.post('/login', {
    email: form.login,
    password: form.pass
  }).then(response => {
    const { token, user } = response.data;
    localStorage.setItem('access_token', token);
    const mainStore = useMainStore()
    mainStore.setUser({ name: user.name, email: user.email })
    axios.defaults.headers.common['Authorization'] = 'Bearer ' + token;
    isLoading.value = false;
    router.push('/dashboard')
  }).catch(error => {
    isLoading.value = false
    console.log('error>>>', error);
  })
}
</script>

<template>
  <LayoutGuest>
    <Loading :is-loading="isLoading" />
    <SectionFullScreen v-slot="{ cardClass }" bg="pinkRed">
      <CardBox :class="cardClass" is-form @submit.prevent="submit">
        <FormField label="Login" help="Please enter your email">
          <FormControl v-model="form.login" :icon="mdiAccount" name="login" autocomplete="username" required />
        </FormField>

        <FormField label="Password" help="Please enter your password">
          <FormControl v-model="form.pass" :icon="mdiAsterisk" type="password" name="password"
            autocomplete="current-password" required />
        </FormField>

        <FormCheckRadio v-model="form.remember" name="remember" label="Remember" :input-value="true" />

        <template #footer>
          <BaseButtons>
            <BaseButton type="submit" color="info" label="Login" />
            <BaseButton to="/dashboard" color="info" outline label="Back" />
          </BaseButtons>

        </template>

      </CardBox>

    </SectionFullScreen>

  </LayoutGuest>
</template>
