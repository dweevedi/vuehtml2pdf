<template>
    <div id="app">
        <div ref="all">
            <button data-html2canvas-ignore="true" @click="download">Download</button>
            <img alt="Vue logo" src="./assets/logo.png" />
            <HelloWorld ref="hello" msg="Welcome to Your Vue.js App" />
            <HelloWorld ref="hello" msg="Welcome to Your Vue.js App" />
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
                var imgData = canvas.toDataURL('image/png');
                var imgWidth = 210;
                var pageHeight = 295;
                var imgHeight = canvas.height * imgWidth / canvas.width;
                var heightLeft = imgHeight;
                var doc = new jsPDF('p', 'mm');
                var position = 10; // give some top padding to first page

                doc.addImage(imgData, 'PNG', 0, position, imgWidth, imgHeight);
                heightLeft -= pageHeight;

                while (heightLeft >= 0) {
                    position += heightLeft - imgHeight; // top padding for other pages
                    doc.addPage();
                    doc.addImage(imgData, 'PNG', 0 , position, imgWidth, imgHeight);
                    heightLeft -= pageHeight;
                }
                doc.save( 'file.pdf');
                /* var imgdata = canvas.toDataURL("image/jpg");
                var doc = new jsPDF();
                doc.addImage(imgdata, "jpg", 10, 10);
                doc.save("hello.pdf"); */
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
