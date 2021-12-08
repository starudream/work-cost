<template>
  <el-row>
    <el-col>
      <el-result icon="error" :title="error.statusCode === 404 ? '页面未找到' : '未知错误'">
        <template slot="extra">
          <el-button type="primary" size="medium" @click="$router.go(-1)">返回</el-button>
        </template>
      </el-result>
    </el-col>
  </el-row>
</template>

<script>
export default {
  props: ["error"],
}
</script>
