<template>
  <el-form :model="form" label-width="120px">
    <el-form-item label="活动 名称">
      <el-input v-model="form.name" />
    </el-form-item>
    <el-form-item label="业务 位置">
      <el-select v-model="form.region" placeholder="please select your zone">
        <el-option label="shanghai" value="shanghai" />
        <el-option label="beijing" value="beijing" />
        <el-option label="guangzhou" value="guangzhou" />
      </el-select>
    </el-form-item>
    <el-form-item label="活动 时间">
      <el-col :span="11">
        <el-date-picker
            v-model="form.date1"
            type="date"
            placeholder="Pick a date"
            style="width: 100%"
        />
      </el-col>
      <el-col :span="2" class="text-center">
        <span class="text-gray-500">-</span>
      </el-col>
      <el-col :span="11">
        <el-time-picker
            v-model="form.date2"
            placeholder="Pick a time"
            style="width: 100%"
        />
      </el-col>
    </el-form-item>
    <el-form-item label="延迟 提交">
      <el-switch v-model="form.delivery" />
    </el-form-item>
    <el-form-item label="活动 形式">
      <el-checkbox-group v-model="form.type">
        <el-checkbox label="线上 活动" name="type" />
        <el-checkbox label="销售 推广" name="type" />
        <el-checkbox label="线下 活动" name="type" />
        <el-checkbox label="营销 介绍" name="type" />
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="资源 申请">
      <el-radio-group v-model="form.resource">
        <el-radio label="赞助商" />
        <el-radio label="地址" />
      </el-radio-group>
    </el-form-item>
    <el-form-item label="活动 形式">
      <el-input v-model="form.desc" type="textarea" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">提交</el-button>
      <el-button>取消</el-button>
    </el-form-item>
  </el-form>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'

// do not use same name with ref
const form = reactive({
  name: '',
  region: '',
  date1: '',
  date2: '',
  delivery: false,
  type: [],
  resource: '',
  desc: '',
})
const onSubmit = () => {
  console.log('submit!')
}
</script>
