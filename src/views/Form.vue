<template>
  <div class="form-container">
    <el-card class="form-card">
      <template #header>
        <div class="card-header">
          <span>多文本框表单</span>
          <el-icon>
            <Document />
          </el-icon>
        </div>
      </template>

      <el-form :model="formData" label-width="120px" class="demo-form">
        <!-- 第一个文本框 -->
        <el-form-item label="文本框 1">
          <div class="textarea-container">
            <el-input v-model="formData.textarea1" type="textarea" :rows="6" placeholder="请输入第一段文本内容..."
              class="textarea-input" />
            <div class="line-counter">
              <el-tag type="info" size="small">
                已输入 {{ textarea1Lines }} 行
              </el-tag>
            </div>
          </div>
        </el-form-item>

        <!-- 第二个文本框 -->
        <el-form-item label="文本框 2">
          <div class="textarea-container">
            <el-input v-model="formData.textarea2" type="textarea" :rows="6" placeholder="请输入第二段文本内容..."
              class="textarea-input" />
            <div class="line-counter">
              <el-tag type="info" size="small">
                已输入 {{ textarea2Lines }} 行
              </el-tag>
            </div>
          </div>
        </el-form-item>

        <!-- 表单操作按钮 -->
        <el-form-item>
          <el-space>
            <el-button type="primary" @click="handleSubmit">
              <el-icon>
                <Check />
              </el-icon>
              提交表单
            </el-button>
            <el-button @click="handleReset">
              <el-icon>
                <Refresh />
              </el-icon>
              重置表单
            </el-button>
          </el-space>
        </el-form-item>
      </el-form>

      <!-- 统计信息展示 -->
      <el-divider />
      <div class="statistics">
        <h3>统计信息</h3>
        <el-row :gutter="20">
          <el-col :span="12">
            <el-card shadow="hover" class="stat-card">
              <div class="stat-content">
                <el-icon class="stat-icon" color="#409eff">
                  <Document />
                </el-icon>
                <div class="stat-text">
                  <div class="stat-title">文本框 1</div>
                  <div class="stat-value">{{ textarea1Lines }} 行</div>
                  <div class="stat-chars">{{ formData.textarea1.length }} 字符</div>
                </div>
              </div>
            </el-card>
          </el-col>
          <el-col :span="12">
            <el-card shadow="hover" class="stat-card">
              <div class="stat-content">
                <el-icon class="stat-icon" color="#67c23a">
                  <Document />
                </el-icon>
                <div class="stat-text">
                  <div class="stat-title">文本框 2</div>
                  <div class="stat-value">{{ textarea2Lines }} 行</div>
                  <div class="stat-chars">{{ formData.textarea2.length }} 字符</div>
                </div>
              </div>
            </el-card>
          </el-col>
        </el-row>
      </div>
    </el-card>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { ElMessage } from 'element-plus'

// 表单数据
const formData = ref({
  textarea1: '',
  textarea2: ''
})

// 计算每个文本框的行数
const textarea1Lines = computed(() => {
  if (!formData.value.textarea1) return 0
  return formData.value.textarea1.split('\n').length
})

const textarea2Lines = computed(() => {
  if (!formData.value.textarea2) return 0
  return formData.value.textarea2.split('\n').length
})

// 表单提交处理
const handleSubmit = () => {
  console.log('表单数据:', formData.value)
  ElMessage.success('表单提交成功！')
}

// 重置表单
const handleReset = () => {
  formData.value = {
    textarea1: '',
    textarea2: ''
  }
  ElMessage.info('表单已重置')
}
</script>

<style scoped>
.form-container {
  padding: 20px;
  max-width: 1000px;
  margin: 0 auto;
}

.form-card {
  margin-bottom: 20px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.demo-form {
  padding: 20px 0;
}

.textarea-container {
  position: relative;
  width: 100%;
}

.textarea-input {
  width: 100%;
}

.line-counter {
  position: absolute;
  top: 8px;
  right: 8px;
  z-index: 10;
}

.statistics {
  margin-top: 20px;
}

.statistics h3 {
  margin-bottom: 20px;
  color: #303133;
  text-align: center;
}

.stat-card {
  height: 120px;
}

.stat-content {
  display: flex;
  align-items: center;
  height: 100%;
}

.stat-icon {
  font-size: 32px;
  margin-right: 16px;
}

.stat-text {
  flex: 1;
}

.stat-title {
  font-size: 14px;
  color: #909399;
  margin-bottom: 8px;
}

.stat-value {
  font-size: 24px;
  font-weight: bold;
  color: #303133;
  margin-bottom: 4px;
}

.stat-chars {
  font-size: 12px;
  color: #909399;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .form-container {
    padding: 10px;
  }

  .stat-content {
    flex-direction: column;
    text-align: center;
  }

  .stat-icon {
    margin-right: 0;
    margin-bottom: 8px;
  }
}
</style>
