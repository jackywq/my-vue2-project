<template>
  <div class="parent-box">
    <h2>父组件</h2>
    <p>状态: {{ loading ? '数据加载中...' : '数据加载完成' }}</p>

    <div style="display: flex; gap: 20px">
      <!-- 对照组：普通子组件 (同步渲染) -->
      <div class="case-box">
        <h3>1. 普通子组件 (Standard)</h3>
        <p>无 v-if，随父组件同步挂载</p>
        <child-component
          name="Standard-Child"
          :parent-data="{ info: '静态数据' }"
        ></child-component>
      </div>

      <!-- 实验组：优化子组件 (异步渲染) -->
      <div class="case-box">
        <h3>2. 优化子组件 (Optimized)</h3>
        <p>有 v-if，等待数据返回后挂载</p>
        <div v-if="!loading" class="child-wrapper">
          <child-component
            name="Optimized-Child"
            :parent-data="fetchedData"
          ></child-component>
        </div>
        <div v-else>⏳ 等待父组件数据...</div>
      </div>
    </div>
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue'

export default {
  components: {
    ChildComponent,
  },
  data() {
    return {
      loading: true,
      fetchedData: null,
    }
  },
  beforeCreate() {
    console.log('Parent beforeCreate')
  },
  created() {
    console.log('Parent created: 发起异步请求')
    this.simulateFetch()
  },
  beforeMount() {
    console.log('Parent beforeMount')
  },
  mounted() {
    console.log('Parent mounted')
  },
  beforeUpdate() {
    console.log('Parent beforeUpdate')
  },
  updated() {
    console.log('Parent updated')
  },
  beforeDestroy() {
    console.log('Parent beforeDestroy')
  },
  destroyed() {
    console.log('Parent destroyed')
  },
  methods: {
    simulateFetch() {
      // 模拟接口请求，延迟 1.5秒
      setTimeout(() => {
        this.fetchedData = {
          id: 1,
          info: '这是父组件获取的重要数据',
        }
        this.loading = false
        console.log('Parent: 数据请求完成 (Data Fetched)')
      }, 1500)
    },
  },
}
</script>

<style scoped>
.parent-box {
  padding: 20px;
  border: 2px solid #333;
  background: #f0f0f0;
}
.case-box {
  flex: 1;
  padding: 10px;
  border: 1px solid #999;
  background: #e6e6e6;
}
.child-wrapper {
  margin-top: 15px;
}
</style>
