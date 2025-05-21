<template>
    <div>
        <ul>
            <li v-for="member in members" :key="member.id"
                class="flex items-center justify-between gap-3 py-3 px-4 sm:px-6">
                <div class="flex items-center gap-3 min-w-0">
                    <UAvatar :src="member.avatar" size="md" />

                    <div class="text-sm min-w-0">
                        <p class="text-highlighted font-medium truncate">
                            {{ member.name }}
                        </p>
                        <p class="text-muted truncate">
                            {{ member.username }}
                        </p>
                    </div>
                </div>
                <div class="flex items-center gap-3">
                    <USelect v-model="member.role" :items="roles" color="neutral"
                        :ui="{ value: 'capitalize', item: 'capitalize' }" />

                    <UDropdownMenu :items="items" :content="{ align: 'end' }">
                        <UButton icon="i-lucide-ellipsis-vertical" color="neutral" variant="ghost" />
                    </UDropdownMenu>
                </div>
            </li>

        </ul>
    </div>
</template>

<script setup>
defineProps({
    members: {
        type: Array,
        required: true,
    },
});

import { reactive } from 'vue'

const member = reactive({
    role: 'member' // or 'owner', whatever the default is
})

const roles = ['member', 'owner']
</script>

<style scoped></style>