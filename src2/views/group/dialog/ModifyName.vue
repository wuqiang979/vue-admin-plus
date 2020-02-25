<template>
  <el-dialog
    title="更新分组"
    :visible.sync="dialogVisible"
    width="500px"
    @close="$emit('update:show', false)"
  >
    <el-form ref="el-form" :model="formData" size="medium" label-width="80px">
      <el-form-item label="分组类型">
        <span>域名转发</span>
      </el-form-item>
      <el-form-item label="分组名称" required>
        <el-input v-model="formData.name" placeholder="分组名称不能为空" />
      </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button size="small" @click="dialogVisible = false">取 消</el-button>
      <el-button size="small" type="primary" @click="submitData">确 定</el-button>
    </span>
  </el-dialog>
</template>

<script>
import { patchGroupInfo } from '@/api/common'
export default {
  components: {},
  props: {
    show: {
      type: Boolean,
      default: false
    },
    opereateData: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      dialogVisible: false,
      formData: {
        name: ''
      }
    }
  },
  watch: {
    show(value) {
      this.dialogVisible = value
      this.formData.name = this.opereateData.name
    }
  },
  created() {

  },
  methods: {
    submitData() {
      if (this.formData.name) {
        patchGroupInfo(this.opereateData.id, this.formData).then(res => {
          this.dialogVisible = false
          this.$message.success(res.message)
          this.$emit('update')
        })
      } else {
        this.$message.warning('请输入分组名称')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.flex-box {
  margin-bottom: 20px;
  @include flex(flex-end);
}
</style>

