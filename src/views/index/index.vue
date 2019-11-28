<template>
  <div id="app-container">
    <el-container>

      <el-container>
      <el-aside style="width:200px">
        <leftBar />
      </el-aside>
      <el-main style="padding: 0">
        <!--<Nav />-->
        <router-view />
      </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script>
  import Nav from "@/components/nav-bar/Navbar.vue";
import leftBar from "@/components/left-bar/index.vue";
export default {
  name: "index",
  components: {
    leftBar,
    Nav
  }
};
</script>

