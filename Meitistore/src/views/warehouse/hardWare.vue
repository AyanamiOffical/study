<template>
  <div>
    <el-table :data="tableData" style="width: 100%" max-height="250">
      <el-table-column fixed prop="goodsNumber" label="货物号" width="150" show-overflow-tooltip />
      <el-table-column prop="goodsName" label="货物名称" width="120" show-overflow-tooltip />
      <el-table-column prop="receiveTime" label="收货时间" width="120" show-overflow-tooltip />
      <el-table-column prop="receiver" label="收货人" width="400" show-overflow-tooltip />
      <el-table-column prop="description" label="货单描述" width="120" show-overflow-tooltip />
      <el-table-column fixed="right" label="操作" width="120">
        <template #default="scope">
          <el-button
              link
              type="primary"
              size="small"
              @click.prevent="deleteRow(scope.$index)"
          >
            移除
          </el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-button class="mt-4" style="width: 100%" @click="showAddDialog">
      添加货物
    </el-button>

    <el-dialog v-model="dialogVisible" title="添加货物">
      <el-form ref="addForm" :model="addItemForm" label-width="80px">
        <el-form-item label="货物号" prop="goodsNumber">
          <el-input v-model="addItemForm.goodsNumber" style="width: 200px;"></el-input>
        </el-form-item>
        <el-form-item label="货物名称" prop="goodsName">
          <el-input v-model="addItemForm.goodsName" style="width: 200px;"></el-input>
        </el-form-item>
        <el-form-item label="收货时间" prop="receiveTime">
          <el-date-picker v-model="addItemForm.receiveTime" type="date" placeholder="选择日期"></el-date-picker>
        </el-form-item>
        <el-form-item label="收货人" prop="receiver">
          <el-input v-model="addItemForm.receiver" style="width: 300px;"></el-input>
        </el-form-item>
        <el-form-item label="货单描述" prop="description">
          <el-input v-model="addItemForm.description" style="width: 150px;"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="addItem">添加</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import dayjs from 'dayjs'

const now = new Date()

const tableData = ref([
  {
    goodsNumber: 'G12345',
    goodsName: '极狐腰带',
    receiveTime: '2024-05-01',
    receiver: '丁 真',
    description: '商品描述...',
  },
  {
    goodsNumber: 'G67890',
    goodsName: '强袭自由',
    receiveTime: '2023-05-02',
    receiver: '五条 吾',
    description: '商品描述...',
  },
  {
    goodsNumber: 'G54321',
    goodsName: '珍珠',
    receiveTime: '2023-12-01',
    receiver: '原神 玩家',
    description: '商品描述...',
  },
])

const deleteRow = (index) => {
  tableData.value.splice(index, 1)
}

const dialogVisible = ref(false)
const addItemForm = ref({
  goodsNumber: '',
  goodsName: '',
  receiveTime: '',
  receiver: '',
  description: '',
})

const showAddDialog = () => {
  dialogVisible.value = true
}

const addItem = () => {
  if (addItemForm.value.goodsNumber && addItemForm.value.goodsName) {
    tableData.value.push({ ...addItemForm.value })
    dialogVisible.value = false
    resetAddItemForm()
  }
}

const resetAddItemForm = () => {
  addItemForm.value = {
    goodsNumber: '',
    goodsName: '',
    receiveTime: '',
    receiver: '',
    description: '',
  }
}
</script>

<style>
/* Add styles if needed */
</style>
