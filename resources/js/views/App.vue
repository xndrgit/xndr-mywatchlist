<template>
    <div class="container-lg dark-mode">
        <HeaderComponent/>
        <router-view></router-view>
        <FooterComponent/>
    </div>
</template>


<script>
import HeaderComponent from "../components/HeaderComponent.vue";
import FooterComponent from "../components/FooterComponent.vue";

import HomePage from "../pages/HomePage.vue";

export default {
    name: 'App',
    components: {
        FooterComponent,
        HeaderComponent,

        HomePage,
    }
}
</script>


<style lang="scss">
// Default styles for light mode
body {
    background-color: #343a40;
    color: #fff;
}

// Styles for dark mode
body.dark-mode {
    background-color: #343a40;
    color: #fff;
}

// Additional styles for dark mode
body.dark-mode h1 {
    color: #fff;
}

body.dark-mode a {
    color: #aaf;
}

body.dark-mode .btn {
    background-color: #aaf;
    color: #333;
}

// Media query to enable dark mode at a certain screen width
@media (min-width: 768px) {
}

</style>
