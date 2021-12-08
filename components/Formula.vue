<template>
  <div class="formula">
    $$工作性价比 = {平均日薪 * (工作环境系数 * 异性环境系数 * 同事环境系数) \over 35 * (工作时长 + 通勤时长 - 0.5 * 摸鱼时长) * 学历系数}$$
  </div>
</template>

<script>
export default {
  head() {
    return {
      script: [
        {src: this.$nuxt.context.env.path + "js/mathjax/tex-svg.js", async: true, body: true},
      ],
    }
  },
}
</script>

<style scoped>
.formula {
  height: 100px;
  overflow-x: auto;
}
</style>
