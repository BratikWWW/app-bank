<template>
  <app-loader v-if="loading"></app-loader>
  <app-page title="Список заявок" v-else>
    <template #header>
      <button class="btn primary" @click="modal = true">Создать</button>
    </template>

    <request-table :requests="requests"></request-table>

    <teleport to="body">
      <app-modal v-if="modal" title="Создать заявку" @close="modal = false">
        <request-modal @created ="modal = false"></request-modal>
      </app-modal>
    </teleport>

  </app-page>
</template>

<script>
import {ref, computed, onMounted} from 'vue'
import AppLoader from '../components/ui/AppLoader'
import RequestTable from '../components/request/RequestTable'
import RequestModal from '../components/request/RequestModal'
import AppPage from '../components/ui/AppPage'
import AppModal from '../components/ui/AppModal'
import { useStore } from 'vuex'
export default {
  setup() {
    const store = useStore()
    const modal = ref(false)
    const loading = ref(false)

    onMounted(async () => {
      loading.value = true
      await store.dispatch('request/load')
      loading.value = false
    })

    const requests = computed(() => store.getters['request/requests'])
    return {
      modal, requests, loading 
    }
  },
  components: {AppPage, RequestTable, AppModal, RequestModal, AppLoader}
}
</script>
