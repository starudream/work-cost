<template>
  <el-row class="row">
    <el-col>
      <el-alert class="result" :title="'得分：'+score+'，工作性价比：'+level" type="info" effect="light" :closable="false" v-if="level!==''"></el-alert>
      <el-form ref="form" :model="form" class="form" label-position="right" label-width="140px" size="mini">
        <el-form-item label="税后月工资+奖金">
          <el-input-number v-model="form.salary" :min="0" :precision="0" :step="100"></el-input-number>
        </el-form-item>
        <el-form-item label="每月工作天数">
          <el-input-number v-model="form.day" :min="0" :precision="2" :step="0.5"></el-input-number>
        </el-form-item>
        <el-form-item label="每日工作时长">
          <el-input-number v-model="form.work" :min="0" :precision="1" :step="0.5"></el-input-number>
        </el-form-item>
        <el-form-item label="每日通勤时长">
          <el-input-number v-model="form.commute" :min="0" :precision="1" :step="0.5"></el-input-number>
        </el-form-item>
        <el-form-item label="每日摸鱼/休息时长">
          <el-input-number v-model="form.rest" :min="0" :precision="1" :step="0.5"></el-input-number>
        </el-form-item>
        <el-form-item label="学历要求">
          <el-select v-model="form.edu" placeholder="请选择">
            <el-option
              v-for="item in eduOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="工作环境">
          <el-select v-model="form.env" placeholder="请选择">
            <el-option
              v-for="item in envOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="身边的异性">
          <el-select v-model="form.sex" placeholder="请选择">
            <el-option
              v-for="item in sexOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="身边的同事">
          <el-select v-model="form.coll" placeholder="请选择">
            <el-option
              v-for="item in collOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="职业资格要求">
          <el-select v-model="form.qua" placeholder="请选择">
            <el-option
              v-for="item in quaOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="经常8:30前上班 24:00后下班" label-width="230px">
          <el-switch v-model="form.over" active-color="#13ce66" inactive-color="#ff4949"></el-switch>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="calculate">计算</el-button>
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>

<script>
export default {
  data() {
    return {
      form:        {
        salary:  10000,
        day:     21.75,
        work:    9,
        commute: 2,
        rest:    1,
        edu:     1,
        env:     1,
        sex:     1,
        coll:    1,
        qua:     1,
        over:    false,
      },
      score:       0,
      level:       "",
      eduOptions:  [
        {label: "专科及以下", value: 0.8},
        {label: "普通本科", value: 1},
        {label: "高级本科", value: 1.2},
        {label: "普通硕士", value: 1.4},
        {label: "高级硕士", value: 1.6},
        {label: "普通博士", value: 1.8},
        {label: "高级博士", value: 2},
      ],
      envOptions:  [
        {label: "偏僻地区", value: 0.8},
        {label: "工厂户外", value: 0.9},
        {label: "普通", value: 1},
        {label: "体制内", value: 1.1},
      ],
      sexOptions:  [
        {label: "没有", value: 0.9},
        {label: "不多不少", value: 1},
        {label: "很多", value: 1.1},
      ],
      collOptions: [
        {label: "SB很多", value: 0.95},
        {label: "普通很多", value: 1},
        {label: "优秀很多", value: 1.05},
      ],
      quaOptions:  [
        {label: "无要求", value: 1},
        {label: "建造造价监理", value: 1.05},
        {label: "建筑岩土结构", value: 1.1},
        {label: "主任医师、教授", value: 1.15},
      ],
    }
  },
  methods: {
    calculate() {
      const form = this.form
      let m = ((form.salary / form.day) * (form.env * form.sex * form.coll * form.qua)) / (35 * (form.work + form.commute + form.rest / 2) * form.edu) * (form.over ? 1 : 0.95)
      this.score = m.toFixed(2)
      this.level = this.score < 0.8 ? "很惨" : this.score < 1.5 ? "一般" : this.score < 2 ? "很爽" : "爽到爆炸"
    },
  },
}
</script>

<style scoped>
.row {
  margin-top: 40px;
}

.result, .form {
  width: 320px;
  margin: 0 auto;
}

.result {
  text-align: center;
  margin-bottom: 20px;
}
</style>
