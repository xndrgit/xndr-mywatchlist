<template>
    <footer class="text-light">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <span>&copy; 2023 My Watch List</span>
                </div>
                <div class="col-md-6 text-md-right">
                    <span><a href="https://github.com/XanderWorld">Privacy Policy</a> | <a
                        href="https://github.com/XanderWorld">Terms of Service</a></span>
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
    height: 10vh;

    display: flex;
    align-items: center;
}
</style>
