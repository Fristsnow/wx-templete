<!--
 * @Author: Lucky-Firstsnow firstsnow1119@163.com
 * @Date: 2024-07-01 16:04:03
 * @LastEditors: Lucky-Firstsnow firstsnow1119@163.com
 * @LastEditTime: 2024-07-03 10:49:36
 * @FilePath: \my-vue3-project\src\pages\index\index.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <view class="content">
    <up-upload :fileList="fileList1" @afterRead="afterRead" @delete="deletePic" name="1" multiple :maxCount="10">
      <image v-if="srcImg" class="image" :src="srcImg" mode="scaleToFill" />
      <image v-else="srcImg" class="image" src="/static/logo.png" mode="scaleToFill" />
    </up-upload>
    <view class="text-area">
      <text class="title">{{ title }}</text>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue';

const title = ref('Hello');
const fileList1 = ref([]);
const srcImg = ref("")
// 删除图片
const deletePic = (event) => {
  fileList1.value.splice(event.index, 1);
};

// 新增图片
const afterRead = async (event) => {
  // 当设置 mutiple 为 true 时, file 为数组格式，否则为对象格式
  let lists = [].concat(event.file);
  let fileListLen = fileList1.value.length;
  lists.map((item) => {
    fileList1.value.push({
      ...item,
      status: 'uploading',
      message: '上传中',
    });
  });
  for (let i = 0; i < lists.length; i++) {
    const result = await uploadFilePromise(lists[i].url);
    let item = fileList1.value[fileListLen];
    fileList1.value.splice(fileListLen, 1, {
      ...item,
      status: 'success',
      message: '',
      url: result,
    });
    fileListLen++;
  }
};

const uploadFilePromise = (url) => {
  return new Promise((resolve, reject) => {
    let a = uni.uploadFile({
      url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
      filePath: url,
      name: 'file',
      formData: {
        user: 'test',
      },
      success: (res) => {
        setTimeout(() => {
          resolve(res.data.data);
          srcImg.value = res.data.data;
        }, 1000);
      },
    });
  });
};
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin-top: 200rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}
</style>
