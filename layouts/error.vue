<template>
    <div>
        <div class="title">
            {{ message }}
        </div>
        <p v-if="statusCode === 404">
            <nuxt-link to="/">Return to homepage</nuxt-link>
        </p>
    </div>
</template>

<script>
export default {
    name: 'NuxtError',
    props: {
        error: {
            type: Object,
            default: null,
        },
    },
    head() {
        return {
            title: this.message,
        }
    },
    computed: {
        statusCode() {
            return (this.error && this.error.statusCode) || 500
        },
        message() {
            return this.error.message
        },
    },
}
</script>
