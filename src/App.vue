<template>
  <div id="app">
    <!-- 优化：使用keep-alive缓存数据，减少每次更换城市时的请求次数 -->
    <!-- 除了detail页面，其他页面均会被缓存 -->
    <keep-alive exclude="Detail">
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>

</style>
