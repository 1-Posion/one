<template>
  <el-breadcrumb separator=">" class="breadcrumb">
    <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
    <el-breadcrumb-item>
      <a href="/">活动管理</a>
    </el-breadcrumb-item>
    <el-breadcrumb-item>活动列表</el-breadcrumb-item>
    <el-breadcrumb-item>活动详情</el-breadcrumb-item>
  </el-breadcrumb>
</template>
<style scoped>
.breadcrumb {
    height:50px;
    line-height: 50px;
    background: #fff;
    padding-left:20px;
}
</style>