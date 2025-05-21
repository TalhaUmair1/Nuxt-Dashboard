<template>
    <UForm id="setting" :schema="profileSchema" :state="profile" class="space-y-4 " @submit="onSubmit">
        <UPageCard title="Profile" description="These informations will be displayed publicly." variant="naked"
            orientation="horizontal" class="mb-4">
            <UButton form="setting" label="Save Changes" color="info" type="submit" class="w-fit lg:ms-auto" />
        </UPageCard>

        <UPageCard variant="subtle" class="border border-orange-500">
            <UFormField name="name" label="Name"
                description="Will appear on receipts, invoices, and other communication." required
                class="flex max-sm:flex-col justify-between items-start gap-4">
                <UInput v-model="profile.name" autocomplete="off" />
            </UFormField>

            <USeparator />

            <UFormField name="email" label="Email"
                description="Will appear on receipts, invoices, and other communication." required
                class="flex max-sm:flex-col justify-between items-start gap-4">
                <UInput v-model="profile.email" type="email" autocomplete="off" />
            </UFormField>

            <USeparator />

            <UFormField name="username" label="Username"
                description="Will appear on receipts, invoices, and other communication." required
                class="flex max-sm:flex-col justify-between items-start gap-4">
                <UInput v-model="profile.username" autocomplete="off" />
            </UFormField>

            <USeparator />

            <UFormField name="avatar" label="Avatar" description="JPG, GIF or PNG. 1MB Max."
                class="flex max-sm:flex-col justify-between sm:items-center gap-4">
                <div class="flex flex-wrap items-center gap-3">
                    <UAvatar :src="profile.avatar" :alt="profile.name" size="lg" />
                    <UButton label="Choose" color="neutral" @click="onFileClick" />
                    <input ref="fileRef" type="file" class="hidden" accept=".jpg, .jpeg, .png, .gif"
                        @change="onFileChange" />
                </div>
            </UFormField>
            <USeparator />
            <UFormField name="bio" label="Bio" description="Brief description for your profile. URLs are hyperlinked."
                class="flex max-sm:flex-col justify-between items-start gap-4" :ui="{ container: 'w-full' }">
                <UTextarea v-model="profile.bio" :rows="5" autoresize class="w-full"
                    placeholder="write about your Bio here" />
            </UFormField>
        </UPageCard>
    </UForm>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import * as z from 'zod'

const profileSchema = z.object({
    name: z.string().min(4, 'Too short, at least 4 characters'),
    email: z.string().email('Invalid email, please enter a valid email'),
    username: z.string().min(4, 'Too short, at least 4 characters'),
    avatar: z.string().optional(),
    bio: z.string().optional()
})

const profile = reactive({
    name: 'Talha Umair',
    email: 'talhaumiargmail.com',
    username: 'umair talha',
    avatar: '',
    bio: ''
})

const fileRef = ref<HTMLInputElement | null>(null)
const toast = useToast()

function onFileClick() {
    fileRef.value?.click()
}

function onFileChange(e: Event) {
    const input = e.target as HTMLInputElement
    if (!input.files || !input.files.length) return

    const file = input.files[0]


    if (!['image/jpeg', 'image/png', 'image/gif'].includes(file.type)) {
        toast.add({
            title: 'Invalid file type',
            description: 'Please upload a JPG, PNG, or GIF file.',
            color: 'warning'
        })
        return
    }


    if (file.size > 1024 * 1024) {
        toast.add({
            title: 'File too large',
            description: 'Max size is 1MB.',
            color: 'warning'
        })
        return
    }


    profile.avatar = URL.createObjectURL(file)
}

async function onSubmit(event: any) {
    toast.add({
        title: 'Success',
        description: 'Your settings have been updated.',
        icon: 'i-lucide-check',
        color: 'success'
    })

    console.log('Form submitted:', event.data)
}
</script>

<style>
/* Optional custom styles here */
</style>
