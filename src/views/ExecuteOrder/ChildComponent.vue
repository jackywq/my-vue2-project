<template>
  <div class="child-box">
    <h4>子组件 ({{ name }})</h4>
    <p>接收到的数据: {{ parentData }}</p>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: 'Child',
    },
    parentData: {
      type: Object,
      default: () => ({}),
    },
  },
  beforeCreate() {
    // 此时无法访问 props，因为组件实例还没初始化完成 props 选项
    console.log(`[Child] beforeCreate`)
  },
  created() {
    console.log(`[${this.name}] created: 获取到 props`, this.parentData)
  },
  beforeMount() {
    console.log(`[${this.name}] beforeMount`)
  },
  mounted() {
    console.log(`[${this.name}] mounted`)
  },
  beforeUpdate() {
    console.log(`[${this.name}] beforeUpdate`)
  },
  updated() {
    console.log(`[${this.name}] updated`)
  },
  beforeDestroy() {
    console.log(`[${this.name}] beforeDestroy`)
  },
  destroyed() {
    console.log(`[${this.name}] destroyed`)
  },
}
</script>

<style scoped>
.child-box {
  border: 2px dashed #666;
  padding: 10px;
  background: #fff;
}
</style>
