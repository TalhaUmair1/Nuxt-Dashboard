<template>
    <USlideover v-model:open="isNotificationsSlideoverOpen" title="Notifications">
        <template #body>
            <NuxtLink v-for="notification in notifications" :key="notification.id" :to="`/inbox?id=${notification.id}`"
                class="px-3 py-2.5 rounded-md hover:bg-elevated/50 flex items-center gap-3 relative -mx-3 first:-mt-3 last:-mb-3">
                <UChip color="error" :show="notification.unread" inset>
                    <UAvatar :src="notification.sender.avatar" :alt="notification.sender.name" size="md" />
                </UChip>

                <div class="text-sm flex-1">
                    <p class="flex items-center justify-between mb-0.5">
                        <span class="text-highlighted font-medium">
                            {{ notification.sender.name }}
                        </span>
                        <time :datetime="notification.date" class="text-muted text-xs"
                            v-text="formatTimeAgo(notification.date)" />
                    </p>
                    <p class="text-dimmed line-clamp-2">
                        {{ notification.body }}
                    </p>
                </div>
            </NuxtLink>
        </template>
    </USlideover>
</template>

<script setup>
const { isNotificationsSlideoverOpen } = useDashboard()

function formatTimeAgo(date) {
    const now = new Date()
    const seconds = Math.floor((now - new Date(date)) / 1000)
    const intervals = {
        year: 31536000,
        month: 2592000,
        week: 604800,
        day: 86400,
        hour: 3600,
        minute: 60,
        second: 1,
    }

    for (const [unit, value] of Object.entries(intervals)) {
        const count = Math.floor(seconds / value)
        if (count > 0) return `${count} ${unit}${count > 1 ? 's' : ''} ago`
    }
    return 'just now'
}

const notifications = ref([
    {
        id: 1,
        sender: {
            avatar: 'https://i.pravatar.cc/300',
            name: 'John Doe',
        },
        body: 'Sent you a message',
        unread: true,
        date: new Date(),
    },
    {
        id: 2,
        sender: {
            avatar: 'https://i.pravatar.cc/301',
            name: 'Jane Doe',
        },
        body: 'You have a new offer!',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 10),
    },
    {
        id: 3,
        sender: {
            avatar: 'https://i.pravatar.cc/302',
            name: 'John Smith',
        },
        body: 'Reminder: your meeting is at 3 PM.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 60 * 3),
    },
    {
        id: 4,
        sender: {
            avatar: 'https://i.pravatar.cc/303',
            name: 'Alice Johnson',
        },
        body: 'Don’t forget to check your task list.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 6),
    },
    {
        id: 5,
        sender: {
            avatar: 'https://i.pravatar.cc/304',
            name: 'Bob Martin',
        },
        body: 'Replied to your comment.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 60 * 12),
    },
    {
        id: 6,
        sender: {
            avatar: 'https://i.pravatar.cc/305',
            name: 'Clara Wilson',
        },
        body: 'Sent a calendar invite.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 60 * 24),
    },
    {
        id: 7,
        sender: {
            avatar: 'https://i.pravatar.cc/306',
            name: 'Daniel Lee',
        },
        body: 'Liked your post.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 48),
    },
    {
        id: 8,
        sender: {
            avatar: 'https://i.pravatar.cc/307',
            name: 'Emily Davis',
        },
        body: 'Shared a file with you.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 30),
    },
    {
        id: 9,
        sender: {
            avatar: 'https://i.pravatar.cc/308',
            name: 'Franklin Knight',
        },
        body: 'Sent you feedback.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 5),
    },
    {
        id: 10,
        sender: {
            avatar: 'https://i.pravatar.cc/309',
            name: 'Grace Hall',
        },
        body: 'Tagged you in a comment.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 90),
    },
    {
        id: 11,
        sender: {
            avatar: 'https://i.pravatar.cc/310',
            name: 'Henry Clark',
        },
        body: 'New task assigned to you.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 20),
    },
    {
        id: 12,
        sender: {
            avatar: 'https://i.pravatar.cc/311',
            name: 'Isabella Lewis',
        },
        body: 'Mentioned you in a team update.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 2),
    },
    {
        id: 13,
        sender: {
            avatar: 'https://i.pravatar.cc/312',
            name: 'Jack White',
        },
        body: 'Commented on your project.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 60 * 7),
    },
    {
        id: 14,
        sender: {
            avatar: 'https://i.pravatar.cc/313',
            name: 'Karen Green',
        },
        body: 'Your request was approved.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 10),
    },
    {
        id: 15,
        sender: {
            avatar: 'https://i.pravatar.cc/314',
            name: 'Leo Walker',
        },
        body: 'Uploaded a new document.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 15),
    },
    {
        id: 16,
        sender: {
            avatar: 'https://i.pravatar.cc/315',
            name: 'Mia Scott',
        },
        body: 'Added you to a group.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 9),
    },
    {
        id: 17,
        sender: {
            avatar: 'https://i.pravatar.cc/316',
            name: 'Nathan Hill',
        },
        body: 'Changed project status.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 60 * 30),
    },
    {
        id: 18,
        sender: {
            avatar: 'https://i.pravatar.cc/317',
            name: 'Olivia Young',
        },
        body: 'Posted an announcement.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 4),
    },
    {
        id: 19,
        sender: {
            avatar: 'https://i.pravatar.cc/318',
            name: 'Paul Allen',
        },
        body: 'Sent a voice note.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 45),
    },
    {
        id: 20,
        sender: {
            avatar: 'https://i.pravatar.cc/319',
            name: 'Quinn Baker',
        },
        body: 'Shared a link with you.',
        unread: false,
        date: new Date(Date.now() - 1000 * 60 * 60 * 13),
    },
    {
        id: 21,
        sender: {
            avatar: 'https://i.pravatar.cc/320',
            name: 'Rachel Morgan',
        },
        body: 'Updated your profile picture.',
        unread: true,
        date: new Date(Date.now() - 1000 * 60 * 2),
    },
])

</script>

<style scoped>
.line-clamp-2 {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
}
</style>
