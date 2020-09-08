<template>
    <div class="home">
        <contactForm />
    </div>
</template>

<script>
import contactForm from './ContactForm'

export default {
    name: 'home',
    components: {
        contactForm
    }
}
</script>

<style lang="sass">
.home
    width: 1200px
    margin: auto
    height: 100vh
    display: flex
</style>