<!--
 * @Author: Lucky-Firstsnow firstsnow1119@163.com
 * @Date: 2024-07-01 16:04:03
 * @LastEditors: Lucky-Firstsnow firstsnow1119@163.com
 * @LastEditTime: 2024-07-03 10:50:24
 * @FilePath: \my-vue3-project\src\pages\index\index.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
    <view>
        <text class="title">{{ title }}</text>
    </view>
</template>

<script setup>
import { ref } from 'vue'
const title = ref("我的")
</script>
<style lang="scss"></style>