<script setup lang="ts">
import { ref } from 'vue'
import { ElMessage } from 'element-plus'

const input = ref('')
const loading = ref(false)
const activeTab = ref('first')

const handleClick = () => {
  loading.value = true
  setTimeout(() => {
    loading.value = false
  }, 2000)
}

const showMessage = (type: 'success' | 'warning' | 'error' | 'info', message: string) => {
  ElMessage[type](message)
}
</script>

<template>
  <div class="home-container">
    <el-card class="welcome-card">
      <template #header>
        <div class="card-header">
          <span>欢迎使用 Element Plus</span>
          <el-icon>
            <Star />
          </el-icon>
        </div>
      </template>

      <div class="demo-section">
        <h2>Element Plus 组件演示</h2>

        <!-- 按钮组件 -->
        <div class="demo-group">
          <h3>按钮组件</h3>
          <el-space>
            <el-button type="primary">主要按钮</el-button>
            <el-button type="success">成功按钮</el-button>
            <el-button type="info">信息按钮</el-button>
            <el-button type="warning">警告按钮</el-button>
            <el-button type="danger">危险按钮</el-button>
          </el-space>
        </div>

        <!-- 输入框组件 -->
        <div class="demo-group">
          <h3>输入框组件</h3>
          <el-input v-model="input" placeholder="请输入内容" style="width: 300px">
            <template #prefix>
              <el-icon>
                <Search />
              </el-icon>
            </template>
          </el-input>
        </div>

        <!-- 加载按钮 -->
        <div class="demo-group">
          <h3>加载状态</h3>
          <el-button type="primary" :loading="loading" @click="handleClick">
            点击加载
          </el-button>
        </div>

        <!-- 消息提示 -->
        <div class="demo-group">
          <h3>消息提示</h3>
          <el-space>
            <el-button @click="showMessage('success', '成功消息')">成功</el-button>
            <el-button @click="showMessage('warning', '警告消息')">警告</el-button>
            <el-button @click="showMessage('error', '错误消息')">错误</el-button>
            <el-button @click="showMessage('info', '信息消息')">信息</el-button>
          </el-space>
        </div>

        <!-- 标签页 -->
        <div class="demo-group">
          <h3>标签页</h3>
          <el-tabs v-model="activeTab" style="width: 100%">
            <el-tab-pane label="用户管理" name="first">
              <p>用户管理内容</p>
            </el-tab-pane>
            <el-tab-pane label="配置管理" name="second">
              <p>配置管理内容</p>
            </el-tab-pane>
            <el-tab-pane label="角色管理" name="third">
              <p>角色管理内容</p>
            </el-tab-pane>
          </el-tabs>
        </div>
      </div>
    </el-card>
  </div>
</template>

<style scoped>
.home-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.welcome-card {
  margin-bottom: 20px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.demo-section {
  padding: 20px 0;
}

.demo-group {
  margin-bottom: 30px;
  padding: 20px;
  border: 1px solid #e4e7ed;
  border-radius: 8px;
  background-color: #fafafa;
}

.demo-group h3 {
  margin-top: 0;
  margin-bottom: 15px;
  color: #409eff;
}

.demo-group h2 {
  text-align: center;
  color: #303133;
  margin-bottom: 30px;
}
</style>
