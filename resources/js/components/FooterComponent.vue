<template>
    <footer class="bg-dark text-light py-3">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <p>&copy; 2023 Netflix Fan Site</p>
                </div>
                <div class="col-md-6 text-md-right">
                    <p><a href="#">Privacy Policy</a> | <a href="#">Terms of Service</a></p>
                </div>
            </div>
        </div>
    </footer>
</template>

<script>
export default {
    mounted() {
        console.log('FooterComponent mounted.')
    }
}
</script>

<style lang="scss" scoped>
footer {
}
</style>
