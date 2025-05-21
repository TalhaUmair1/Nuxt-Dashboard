<template>

    <UPageCard title="Password " description="Confirm your current password before setting a new one.">
        <UForm :schema="schema" :state="state" class="space-y-4" @submit="onSubmit">
            <UFormField label="Email" name="email">
                <UInput class="w-[310px]" v-model="state.email" />
            </UFormField>

            <UFormField label="Password" name="password">
                <UInput class="w-[310px]" v-model="state.password" type="password" />
            </UFormField>

            <UButton type="submit">
                Update Password
            </UButton>
        </UForm>
    </UPageCard>

    <UPageCard title="Account"
        description="No longer want to use our service? You can delete your account here. This action is not reversible. All information related to this account will be deleted permanently."
        class="bg-gradient-to-tl from-error/10 from-5% to-default">
        <template #footer>
            <UButton label="Delete account" color="error" />
        </template>
    </UPageCard>

</template>

<script setup lang="ts">
import * as v from 'valibot'
import type { FormSubmitEvent } from '@nuxt/ui'

const schema = v.object({
    email: v.pipe(v.string(), v.email('Required')),
    password: v.pipe(v.string(), v.minLength(8, 'Must be at least 6 characters'))
})

type Schema = v.InferOutput<typeof schema>

const state = reactive({
    email: '',
    password: ''
})

const toast = useToast()
async function onSubmit(event: FormSubmitEvent<Schema>) {
    toast.add({ title: 'Success', description: 'The form has been submitted.', color: 'success' })
    console.log(event.data)
}
</script>

<style lang="scss" scoped></style>