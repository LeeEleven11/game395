<template>
  <div id="app">
    <h1 class="text-2xl font-bold mb-4">S3 任务操作</h1>

    <!-- 任务 1 输入表单 -->
    <div class="mb-4">
      <h2 class="text-lg font-bold mb-2">任务 1</h2>
      <button
        @click="submitTask1"
        class="bg-yellow-500 text-white p-2 rounded hover:bg-yellow-600"
      >
        提交任务 1
      </button>
      <div v-if="task1Result" class="mt-2">
        <h3 class="text-md font-bold">任务 1 结果:</h3>
        <pre class="bg-gray-100 p-2">{{ task1Result }}</pre>
      </div>
    </div>

    <!-- 任务 2 输入表单 -->
    <div class="mb-4">
      <h2 class="text-lg font-bold mb-2">任务 2: 复制 S3 文件</h2>
      <label for="sourceS3URI" class="block mb-1">Source file S3URI:</label>
      <input
        v-model="sourceS3URI"
        type="text"
        id="sourceS3URI"
        class="border border-gray-300 p-2 w-full mb-2"
      />
      <label for="destinationS3URI" class="block mb-1">Destination S3URI:</label>
      <input
        v-model="destinationS3URI"
        type="text"
        id="destinationS3URI"
        class="border border-gray-300 p-2 w-full mb-2"
      />
      <button
        @click="submitTask2"
        class="bg-blue-500 text-white p-2 rounded hover:bg-blue-600"
      >
        提交任务 2
      </button>
      <div v-if="task2Result" class="mt-2">
        <h3 class="text-md font-bold">任务 2 结果:</h3>
        <pre class="bg-gray-100 p-2">{{ task2Result }}</pre>
      </div>
    </div>

    <!-- 任务 3 输入表单 -->
    <div>
      <h2 class="text-lg font-bold mb-2">任务 3: 账户信息查询</h2>
      <label for="account" class="block mb-1">Account:</label>
      <input
        v-model="account"
        type="text"
        id="account"
        class="border border-gray-300 p-2 w-full mb-2"
      />
      <button
        @click="submitTask3"
        class="bg-green-500 text-white p-2 rounded hover:bg-green-600"
      >
        提交任务 3
      </button>
      <div v-if="task3Result" class="mt-2">
        <h3 class="text-md font-bold">任务 3 结果:</h3>
        <pre class="bg-gray-100 p-2">{{ task3Result }}</pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

// 定义响应式变量
const sourceS3URI = ref('');
const destinationS3URI = ref('');
const account = ref('');
const task1Result = ref(null);
const task2Result = ref(null);
const task3Result = ref(null);

// 提交任务 1
const submitTask1 = async () => {
  try {
    const response = await axios.post('/api/task1');
    task1Result.value = JSON.stringify(response.data, null, 2);
  } catch (error) {
    task1Result.value = `错误: ${error.message}`;
  }
};

// 提交任务 2
const submitTask2 = async () => {
  try {
    const response = await axios.post('/api/task2', {
      sourceS3URI: sourceS3URI.value,
      destinationS3URI: destinationS3URI.value,
    });
    task2Result.value = JSON.stringify(response.data, null, 2);
  } catch (error) {
    task2Result.value = `错误: ${error.message}`;
  }
};

// 提交任务 3
const submitTask3 = async () => {
  try {
    const response = await axios.post('/api/task3', {
      account: account.value,
    });
    task3Result.value = JSON.stringify(response.data, null, 2);
  } catch (error) {
    task3Result.value = `错误: ${error.message}`;
  }
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>    