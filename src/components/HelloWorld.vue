<template>
    <div id="app">
        <div class="content">
            <div class="top-bar">
                <div id="navigation-icon" v-if="mobileView">
                    <i class="fas fa-bars"></i>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "HelloWorld",
        props: {
            msg: String,
        },
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
