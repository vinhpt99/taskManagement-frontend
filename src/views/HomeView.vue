<script setup>
import { ref, onMounted } from 'vue'
import {
  mdiChartTimelineVariant,
  mdiCheck,
  mdiCommentAlert
} from '@mdi/js'
import * as chartConfig from '@/components/Charts/chart.config.js'
import SectionMain from '@/components/SectionMain.vue'
import CardBoxWidget from '@/components/CardBoxWidget.vue'
import LayoutAuthenticated from '@/layouts/LayoutAuthenticated.vue'
import SectionTitleLineWithButton from '@/components/SectionTitleLineWithButton.vue'


const chartData = ref(null)

const fillChartData = () => {
  chartData.value = chartConfig.sampleChartData()
}

onMounted(() => {
  fillChartData()
})

// const mainStore = useMainStore()

// const clientBarItems = computed(() => mainStore.clients.slice(0, 4))

// const transactionBarItems = computed(() => mainStore.history)
</script>

<template>
  <LayoutAuthenticated>
    <SectionMain>
      <SectionTitleLineWithButton :icon="mdiChartTimelineVariant" title="Overview" main>
      </SectionTitleLineWithButton>

      <div class="grid grid-cols-1 gap-6 lg:grid-cols-3 mb-6">
        <CardBoxWidget trend="12%" trend-type="up" color="text-emerald-500" :icon="mdiCheck" :number="512" label="Done" />
        <CardBoxWidget trend="12%" trend-type="down" color="text-blue-500" :icon="mdiCommentAlert" :number="7770"
          label="Not Done" />
        <CardBoxWidget trend="Overflow" trend-type="alert" color="text-red-500" :icon="mdiChartTimelineVariant"
          :number="256" suffix="%" label="Total" />
      </div>

      <!-- <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-6">
        <div class="flex flex-col justify-between">
          <CardBoxTransaction v-for="(transaction, index) in transactionBarItems" :key="index"
            :amount="transaction.amount" :date="transaction.date" :business="transaction.business"
            :type="transaction.type" :name="transaction.name" :account="transaction.account" />
        </div>
        <div class="flex flex-col justify-between">
          <CardBoxClient v-for="client in clientBarItems" :key="client.id" :name="client.name" :login="client.login"
            :date="client.created" :progress="client.progress" />
        </div>
      </div>
      <SectionTitleLineWithButton :icon="mdiChartPie" title="Trends overview">
        <BaseButton :icon="mdiReload" color="whiteDark" @click="fillChartData" />
      </SectionTitleLineWithButton>



      <SectionTitleLineWithButton :icon="mdiAccountMultiple" title="Clients" />

      <CardBox has-table>
        <TableSampleClients />
      </CardBox> -->
    </SectionMain>
  </LayoutAuthenticated>
</template>
