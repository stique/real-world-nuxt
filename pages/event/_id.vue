<template>
    <div>
        <h1>{{ event.title }}</h1>
    </div>
</template>

<script>
export default {
    head() {
        return {
            title: `Event #${this.event.title}`,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: `What you need to know about ${this.event.title}`,
                },
            ],
        }
    },

    async asyncData({ $axios, error, params: { id } }) {
        try {
            const response = await $axios.get(
                `http://localhost:3334/events/${id}`
            )

            return {
                event: response.data,
            }
        } catch {
            error({
                statusCode: 503,
                message: `Unable to fetch event #${id}.`,
            })
        }
    },
}
</script>
