<template>
  <div id="app">
    <Header />
    <div class="section">
      <div class="menu">
        <Menu />
      </div>
      <div class="view">
        <Breadcrumb />
        <router-view />
        <!-- <Pagination /> -->
      </div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/header";
import Menu from "@/components/menu";
import Breadcrumb from "@/components/breadcrumb";
import Pagination from "@/components/pagination";
export default {
  name: "App",
  components: { Header, Menu, Breadcrumb, Pagination }
};
</script>

<style>
body {
  margin:0 !important;
  background: #EBEEF5;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

.section {
  display: flex;
}
.menu {
  flex: 1;
  background: #fff !important;
  height:calc(100vh - 60px);
  width:calc(100vh - 333px);
  min-width:200px;
}
.view {
  flex: 9;
}
</style>
