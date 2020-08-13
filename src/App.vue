<template>
    <div id="app">
        <div ref="all">
            <button data-html2canvas-ignore="true" @click="download">Download</button>
            <img alt="Vue logo" src="./assets/logo.png" />
            <HelloWorld ref="hello" msg="Welcome to Your Vue.js App" />
        </div>
    </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { jsPDF } from "jspdf";

export default {
    name: "App",
    components: {
        HelloWorld,
    },
    methods: {
        download() {
            window.html2canvas(this.$refs.all).then((canvas) => {
                var imgdata = canvas.toDataURL("image/jpg");
                var doc = new jsPDF();
                doc.addImage(imgdata, "jpg", 10, 10);
                doc.save("hello.pdf");
            });
        },
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    width: 800px;
}
</style>
