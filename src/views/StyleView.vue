<script setup>
import { useRouter } from 'vue-router'
import { onMounted } from 'vue'
import { useDarkModeStore } from '@/stores/darkMode.js'

const darkModeStore = useDarkModeStore()
darkModeStore.set(false)

const router = useRouter()


const handleStyleChange = (slug) => {
  document.documentElement.classList.forEach((token) => {
    if (token.indexOf('style') === 0) {
      document.documentElement.classList.replace(token, `style-${slug}`)
    }
  })
  router.push('/dashboard')
}
onMounted(() => {
  handleStyleChange('basic');
})
</script>
