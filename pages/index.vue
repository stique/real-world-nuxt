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
    asyncData({ $axios, error }) {
        return $axios
            .get('http://localhost:3334/events')
            .then((response) => {
                return {
                    events: response.data,
                }
            })
            .catch((e) => {
                error({
                    statusCode: 503,
                    message: 'Unable to fetch events.',
                })
            })
    },
}
</script>
