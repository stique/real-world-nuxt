<template>
    <div>
        <h1>Events</h1>
        <EventCard
            v-for="(event, index) in events"
            :key="index"
            :event="event"
            :data-index="index"
        />
    </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
    head() {
        return {
            title: 'Event Listing',
            meta: [
                {
                    hid: 'description',
                    name: 'description', // <-- for our meta description tag
                    content:
                        'Where you can find all the events taking place in your neighborhood',
                },
            ],
        }
    },
    async fetch({ store, error }) {
        try {
            await store.dispatch('events/fetchEvents')
        } catch {
            error({
                statusCode: 503,
                message: 'Unable to fetch events.',
            })
        }
    },
    computed: mapState({
        events: (state) => state.events.events,
    }),
}
</script>
