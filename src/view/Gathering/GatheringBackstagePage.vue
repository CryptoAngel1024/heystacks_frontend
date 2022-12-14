<script lang="ts" setup>
import { ref, watch } from 'vue'

import LayoutDark from '@/layouts/LayoutDark.vue'

import NavTab from '@/components/atoms/NavTab.vue'
import HeaderNav from '@/components/layoutElements/HeaderNav.vue'
import HeaderContent from '@/components/layoutElements/HeaderContent.vue'
import Footer from '@/components/layoutElements/Footer.vue'
import VoteTab from '@/components/backstage/VoteTab.vue'
import ChatTab from '@/components/backstage/ChatTab.vue'
import FinanceTab from '@/components/backstage/FinanceTab.vue'

import { useRoute } from 'vue-router'

// consts
const route = useRoute()
const gatheringSlug = route.params.gatheringSlug.toString()
const tabs = ['Vote', 'Chat', 'Finance']

// state
const selectedTab = ref(route?.query?.tab?.toString() ?? 'Vote')

// watchers
watch(selectedTab, newTab => {
  window.history.replaceState(
    { page: 'heystacks' },
    'heystacks',
    `/g/${gatheringSlug}/backstage?tab=${newTab}`
  )
})
</script>
<template>
  <LayoutDark>
    <template #header-nav>
      <HeaderNav />
    </template>
    <template #header-content>
      <HeaderContent :navLink="{ label: '< Public', path: `/g/${gatheringSlug}` }" />
    </template>
    <template #command-band>
      <div class="mx-auto max-w-screen-md text-center flex-center">
        <NavTab
          v-for="tab in tabs"
          :key="`tab-${tab}`"
          :text="tab"
          :selected="tab === selectedTab"
          @click="selectedTab = tab"
        />
      </div>
    </template>
    <template #content>
      <div class="pt-10 mb-12">
        <VoteTab v-if="selectedTab === 'Vote'" />
        <ChatTab v-if="selectedTab === 'Chat'" />
        <FinanceTab v-if="selectedTab === 'Finance'" />
      </div>
    </template>
    <template #footer>
      <Footer />
    </template>
  </LayoutDark>
</template>
