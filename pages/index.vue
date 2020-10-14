<template>
    <div>
        <h1>Events</h1>
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
}
</script>
