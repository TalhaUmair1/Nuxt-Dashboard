<template>
    <div>
        <UPageCard title="Members" description="Invite new members by email address." variant="naked"
            orientation="horizontal" class="mb-4">
            <UButton label="Invite people" color="warning" class="w-fit lg:ms-auto" />
        </UPageCard>
        <UPageCard variant="subtle"
            :ui="{ container: 'p-0 sm:p-0 gap-y-0', wrapper: 'items-stretch', header: 'p-4 mb-0 border-b border-default' }">
            <template #header>
                <UInput v-model="q" icon="i-lucide-search" placeholder="Search members" autofocus class="w-full" />
            </template>

            <SettingsMembersList :members="filteredMembers" />
        </UPageCard>
    </div>
</template>

<script setup>


const members = [
    {
        id: 1,
        name: 'John Doe',
        username: 'johndoe',
        avatar: 'https://i.pravatar.cc/150?u=1',
    },
    {
        id: 2,
        name: 'Jane Smith',
        username: 'janesmith',
        avatar: 'https://i.pravatar.cc/150?u=2',
    },
    {
        id: 3,
        name: 'Alice Johnson',
        username: 'alicejohnson',
        avatar: 'https://i.pravatar.cc/150?u=3',
    },
    {
        id: 4,
        name: 'Bob Brown',
        username: 'bobbrown',
        avatar: 'https://i.pravatar.cc/150?u=4',
    },
    {
        id: 5,
        name: 'Charlie Davis',
        username: 'charliedavis',
        avatar: 'https://i.pravatar.cc/150?u=5',
    },
    {
        id: 6,
        name: 'Diana Evans',
        username: 'dianaevans',
        avatar: 'https://i.pravatar.cc/150?u=6',
    },
    {
        id: 7,
        name: 'Ethan Foster',
        username: 'ethanfoster',
        avatar: 'https://i.pravatar.cc/150?u=7',
    },
    {
        id: 8,
        name: 'Fiona Green',
        username: 'fionagreen',
        avatar: 'https://i.pravatar.cc/150?u=8',
    },
    {
        id: 9,
        name: 'George Harris',
        username: 'georgeharris',
        avatar: 'https://i.pravatar.cc/150?u=9',
    },
    {
        id: 10,
        name: 'Hannah Ives',
        username: 'hannahives',
        avatar: 'https://i.pravatar.cc/150?u=10',
    },
    {
        id: 11,
        name: 'Ian Johnson',
        username: 'ianjohnson',
        avatar: 'https://i.pravatar.cc/150?u=11',
    },
    {
        id: 12,
        name: 'Jack King',
        username: 'jackking',
        avatar: 'https://i.pravatar.cc/150?u=12',
    },
];
const q = ref('')

const filteredMembers = computed(() => {
    return members.filter((member) => {
        return member.name.search(new RegExp(q.value, 'i')) !== -1 || member.username.search(new RegExp(q.value, 'i')) !== -1
    })
})
</script>

<style scoped></style>