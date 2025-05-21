<template>
    <div v-for="section in sections" :key="section.title" class="mb-8 border border-orange-500 rounded-lg p-4">
        <UPageCard :title="section.title" :description="section.description" variant="naked" class="mb-4" />
        <UPageCard class="border border-primary" variant="subtle" :ui="{ container: 'divide-y divide-default' }">
            <UFormField v-for="field in section.fields" :key="field.name" :name="field.name" :label="field.label"
                :description="field.description" class="flex items-center justify-between not-last:pb-4 gap-2">
                <template #default="{ id }">
                    <USwitch :id="id" v-model="state[field.name]" @update:model-value="onSubmit" />
                </template>
            </UFormField>
        </UPageCard>
    </div>
</template>

<script setup>
const state = reactive({
    email: true,
    desktop: false,
    product_updates: true,
    weekly_digest: false,
    important_updates: true
})

const sections = [
    {
        title: 'Email Notifications',
        description: 'Where can we notify you?',
        fields: [
            { name: 'email', label: 'Email', description: 'Receive a daily email digest.' },
            { name: 'desktop', label: 'Desktop', description: 'Receive desktop notifications.' },
            { name: 'mobile', label: 'Mobile', description: 'Receive mobile notifications.' }
        ]
    },
    {
        title: 'Accounts Updates',
        description: 'Receive updates about Nuxt UI',
        fields: [
            { name: 'weekly_digest', label: 'Weekly digest', description: 'Receive a weekly digest of news.' },
            { name: 'product_updates', label: 'Product updates', description: 'Receive a monthly email with all new features and updates.' },
            { name: 'important_updates', label: 'Important updates', description: 'Receive emails about important updates like security fixes, maintenance, etc.' },
            { name: 'other', label: 'Other', description: 'Receive emails about other important updates.' }
        ]
    }
]

const onSubmit = () => {
    console.log('Form submitted with state:', state)
}
</script>

<style scoped></style>
