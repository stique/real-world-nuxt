<template>
    <div>
        <h1>{{ event.title }}</h1>
    </div>
</template>

<script>
import { mapState } from 'vuex'

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

    async fetch({ store, error, params: { id } }) {
        try {
            await store.dispatch('events/fetchEvent', id)
        } catch {
            error({
                statusCode: 503,
                message: `Unable to fetch event #${id}.`,
            })
        }
    },

    computed: mapState({
        event: (state) => state.events.event,
    }),
}
</script>
