<template>
  <div>
    <el-card>
      <div slot="header">
        <h2>仓库货单</h2>
      </div>
      <el-button type="primary" @click="showDialog">添加</el-button>
      <el-button type="danger" @click="showDeleteDialog">删除</el-button>
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="id" label="序号" width="120"></el-table-column>
        <el-table-column prop="productName" label="货品名称"></el-table-column>
        <el-table-column prop="productCategory" label="货品类别"></el-table-column>
        <el-table-column prop="productWeight" label="货品重量"></el-table-column>
        <el-table-column prop="inStockTime" label="进库时间"></el-table-column>
        <el-table-column prop="outStockTime" label="出库时间"></el-table-column>
        <el-table-column label="操作" width="100">
          <template slot-scope="scope">
            <el-button type="text" @click="editItem(scope.row)">编辑</el-button>
            <el-button type="text" @click="removeItem(scope.$index)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>

      <el-dialog v-model="dialogVisible" title="添加货单">
        <el-form ref="formData" :model="form" label-width="80px">
          <el-form-item label="货品名称" prop="productName">
            <el-input v-model="form.productName"></el-input>
          </el-form-item>
          <el-form-item label="货品类别" prop="productCategory">
            <el-input v-model="form.productCategory"></el-input>
          </el-form-item>
          <el-form-item label="货品重量" prop="productWeight">
            <el-input v-model.number="form.productWeight"></el-input>
          </el-form-item>
          <el-form-item label="进库时间" prop="inStockTime">
            <el-input v-model="form.inStockTime"></el-input>
          </el-form-item>
          <el-form-item label="出库时间" prop="outStockTime">
            <el-input v-model="form.outStockTime"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogVisible = false">取消</el-button>
          <el-button type="primary" @click="saveItem">保存</el-button>
        </div>
      </el-dialog>

      <el-dialog v-model="deleteDialogVisible" title="确认删除">
        <el-form ref="deleteFormData" :model="form" label-width="80px">
          <el-form-item label="货品名称" prop="productName">
            <el-input v-model="deleteProductName"></el-input>
          </el-form-item>
        </el-form>
        <span>是否删除？</span>
        <div slot="footer" class="dialog-footer">
          <el-button @click="deleteDialogVisible = false">取消</el-button>
          <el-button type="danger" @click="confirmRemoveItem">是</el-button>
        </div>
      </el-dialog>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          id: 1,
          productName: '极狐腰带',
          productCategory: '服饰',
          productWeight: 2.5,
          inStockTime: '2023-01-01',
          outStockTime: '2023-01-10',
        },
        {
          id: 2,
          productName: '强袭自由',
          productCategory: '电子产品',
          productWeight: 1.8,
          inStockTime: '2023-02-15',
          outStockTime: '2023-03-01',
        },
        {
          id: 3,
          productName: '珍珠',
          productCategory: '珠宝',
          productWeight: 0.5,
          inStockTime: '2023-04-05',
          outStockTime: '2023-05-01',
        },
      ],
      dialogVisible: false,
      form: {
        productName: '',
        productCategory: '',
        productWeight: 0,
        inStockTime: '',
        outStockTime: '',
      },
      deleteDialogVisible: false,
      deleteProductName: null,
    };
  },
  methods: {
    showDialog() {
      this.dialogVisible = true;
    },
    saveItem() {
      if (this.$refs.formData.validate()) {
        this.tableData.push({ ...this.form, id: this.tableData.length + 1 });
        this.dialogVisible = false;
        this.resetForm();
      }
    },
    resetForm() {
      this.form = {
        productName: '',
        productCategory: '',
        productWeight: 0,
        inStockTime: '',
        outStockTime: '',
      };
    },
    editItem(row) {
      console.log('Edit item:', row);
      // Implement editing logic if needed
    },
    removeItem(index) {
      this.tableData.splice(index, 1);
    },
    showDeleteDialog() {
      this.deleteDialogVisible = true;
    },
    confirmRemoveItem() {
      const index = this.tableData.findIndex(
          (item) => item.productName === this.deleteProductName
      );
      if (index !== -1) {
        this.tableData.splice(index, 1);
      }
      this.deleteProductName = null;
      this.deleteDialogVisible = false;
    },
  },
};
</script>

<style>
/* Add styles if needed */
</style>
