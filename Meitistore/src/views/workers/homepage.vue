<template>
  <el-button @click="resetDateFilter">reset date filter</el-button>
  <el-button @click="clearFilter">reset all filters</el-button>

  <el-table ref="tableRef" row-key="index" :data="tableData" style="width: 100%">
    <el-table-column label="序号" width="80">
      <template #default="scope">
        {{ scope.$index + 1 }}
      </template>
    </el-table-column>
    <el-table-column
        prop="name"
        label="人员名称"
        sortable
        width="180"
    />
    <el-table-column
        prop="age"
        label="年龄"
        sortable
        width="80"
    />
    <el-table-column
        prop="gender"
        label="性别"
        sortable
        width="80"
    />
    <el-table-column
        prop="address"
        label="地址"
        :formatter="formatter"
    />
    <el-table-column
        prop="workTime"
        label="工作时间"
        sortable
        width="120"
    />
    <el-table-column
        prop="date"
        label="Date"
        sortable
        width="180"
        column-key="date"
        :filters="[
        { text: '2023-11-27', value: '2023-11-27' },
        { text: '2023-11-28', value: '2023-11-28' },
      ]"
        :filter-method="filterHandler"
    />
    <el-table-column
        prop="tag"
        label="Tag"
        width="100"
        :filters="[
        { text: 'Ware', value: 'Ware' },
        { text: 'Office', value: 'Office' },
      ]"
        :filter-method="filterTag"
        filter-placement="bottom-end"
    >
      <template #default="scope">
        <el-tag
            :type="scope.row.tag === 'Home' ? '' : 'success'"
            disable-transitions
        >{{ scope.row.tag }}</el-tag
        >
      </template>
    </el-table-column>
  </el-table>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import type { TableColumnCtx, TableInstance } from 'element-plus'

interface User {
  index: number
  name: string
  age: number
  gender: string
  address: string
  workTime: string
  date: string
  tag: string
}

const tableRef = ref<TableInstance>()

const resetDateFilter = () => {
  tableRef.value!.clearFilter(['date'])
}
const clearFilter = () => {
  // eslint-disable-next-line @typescript-eslint/ban-ts-comment
  // @ts-expect-error
  tableRef.value!.clearFilter()
}
const formatter = (row: User, column: TableColumnCtx<User>) => {
  return row.address
}
const filterTag = (value: string, row: User) => {
  return row.tag === value
}
const filterHandler = (
    value: string,
    row: User,
    column: TableColumnCtx<User>
) => {
  const property = column['property']
  return row[property] === value
}

const tableData: User[] = [
  {
    index: 1,
    name: '张三',
    age: 25,
    gender: '男',
    address: '河北省廊坊市',
    workTime: '9:00 AM - 5:00 PM',
    date: '2023-11-27',
    tag: 'Ware',
  },
  {
    index: 2,
    name: '电猫',
    age: 30,
    gender: '女',
    address: '重庆市市区',
    workTime: '8:00 AM - 4:00 PM',
    date: '2023-11-28',
    tag: 'Office',
  },
  {
    index: 3,
    name: '饮月君',
    age: 28,
    gender: '男',
    address: '北京市海淀区',
    workTime: '10:00 AM - 6:00 PM',
    date: '2023-11-28',
    tag: 'Ware',
  },
  {
    index: 4,
    name: 'Tom',
    age: 22,
    gender: '男',
    address: 'No. 189, Grove St, Los Angeles',
    workTime: '9:30 AM - 5:30 PM',
    date: '2023-11-27',
    tag: 'Office',
  },
]
</script>

<style scoped>
</style>
