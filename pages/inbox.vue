<script setup>
import { computed, ref, watch } from 'vue'
import { useBreakpoints, breakpointsTailwind } from '@vueuse/core'

const tabItems = [
    { label: 'All', value: 'all' },
    { label: 'Unread', value: 'unread' }
]
const selectedTab = ref('all')

const { data: mails } = await useFetch('/api/mails', { default: () => [] })

const filteredMails = computed(() => {
    if (selectedTab.value === 'unread') {
        return mails.value.filter(mail => !!mail.unread)
    }

    return mails.value
})

const selectedMail = ref(null)

const isMailPanelOpen = computed({
    get() {
        return !!selectedMail.value
    },
    set(value) {
        if (!value) {
            selectedMail.value = null
        }
    }
})

watch(filteredMails, () => {
    if (!filteredMails.value.find(mail => mail.id === selectedMail.value?.id)) {
        selectedMail.value = null
    }
})

const breakpoints = useBreakpoints(breakpointsTailwind)
const isMobile = breakpoints.smaller('lg')
</script>

<template>
    <UDashboardPanel id="inbox-1" :default-size="25" :min-size="20" :max-size="30" resizable>
        <UDashboardNavbar title="Inbox">
            <template #leading>
                <UDashboardSidebarCollapse />
            </template>

            <template #trailing>
                <UBadge :label="filteredMails.length" variant="subtle" />
            </template>

            <template #right>
                <UTabs v-model="selectedTab" :items="tabItems" class="w-32" :content="false" size="xs" />
            </template>
        </UDashboardNavbar>

        <InboxList v-model="selectedMail" :mails="filteredMails" />
    </UDashboardPanel>

    <InboxMail v-if="selectedMail" :mail="selectedMail" @close="selectedMail = null" />

    <div v-else class="hidden lg:flex flex-1 items-center justify-center">
        <UIcon name="i-lucide-inbox" class="size-32 text-dimmed" />
    </div>

    <ClientOnly>
        <USlideover v-if="isMobile" v-model:open="isMailPanelOpen">
            <template #content>
                <InboxMail v-if="selectedMail" :mail="selectedMail" @close="selectedMail = null" />
            </template>
        </USlideover>
    </ClientOnly>
</template>
