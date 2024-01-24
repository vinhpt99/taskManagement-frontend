<script setup>
import { mdiTableBorder, mdiCalendarPlus } from '@mdi/js'
import SectionMain from '@/components/SectionMain.vue'
import TableSampleClients from '@/components/TableSampleClients.vue'
import CardBox from '@/components/CardBox.vue'
import LayoutAuthenticated from '@/layouts/LayoutAuthenticated.vue'
import SectionTitleLineWithButton from '@/components/SectionTitleLineWithButton.vue'
import BaseButton from '@/components/BaseButton.vue'
import CardBoxModal from '@/components/CardBoxModal.vue'
import { ref, reactive } from 'vue'
import FormField from '@/components/FormField.vue'
import FormControl from '@/components/FormControl.vue'
import { fields } from '@/attribute.js';
import axios from '@/common/axios-instance';


const isModalDangerActive = ref(false)
const isLoading = ref(false)
const formAddTaskFields = reactive([...fields])

const addTask = () => {
  const payload = formAddTaskFields.map((field) => {
    const item = { key: field.key, value: field.value }
    return item
  });
  isLoading.value = true
  console.log('axios>>>', axios);
  axios.post('/addTask', {
    payload
  }).then(response => {
    // const { token, user } = response.data;
    // localStorage.setItem('access_token', token);
    // const mainStore = useMainStore()
    // mainStore.setUser({ name: user.name, email: user.email })
    // axios.defaults.headers.common['Authorization'] = 'Bearer ' + token;
    // isLoading.value = false;
    // router.push('/dashboard')
  }).catch(error => {
    isLoading.value = false
    console.log('error>>>', error);
  })
}
</script>

<template>
  <LayoutAuthenticated>
    <SectionMain>
      <SectionTitleLineWithButton :icon="mdiTableBorder" title="Task Management" main>
        <BaseButton color="success" type="submit" :icon="mdiCalendarPlus" small @click="isModalDangerActive = true" />
      </SectionTitleLineWithButton>
      <CardBox class="mb-6" has-table>
        <TableSampleClients checkable />
      </CardBox>
      <CardBoxModal v-model="isModalDangerActive" title="Add task" is-form size="large" button="success" has-cancel
        @confirm="addTask()">
        <FormField v-for="(field, index) in formAddTaskFields" :key="index">
          <FormField :label="field.label">
            <FormControl v-model="field.value" :type="field.type" :placeholder="field.placeholder" required
              :class="(field.type === `date`) ? `input_date` : ``" />
          </FormField>
        </FormField>
      </CardBoxModal>
    </SectionMain>
  </LayoutAuthenticated>
</template>
<style>
.input_date {
  width: 50%;
}
</style>
