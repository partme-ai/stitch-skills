<template>
  <view class="page-stitch">
    <!-- Replace with u-navbar, u-row/u-col, u-button, etc. per references/contract.md -->
    <u-navbar title="StitchPage" :autoBack="true" @leftClick="onBack" />
    <u-gap height="20" bgColor="#f3f4f6"></u-gap>
    <u-form :model="form" ref="uForm">
      <u-form-item label="Label" prop="name" borderBottom>
        <u-input v-model="form.name" border="none" placeholder="Please input"></u-input>
      </u-form-item>
    </u-form>
    <u-button type="primary" text="Submit" @click="onSubmit" />
  </view>
</template>

<script setup lang="ts">
/**
 * Replace StitchPage with actual page name.
 * Use uView Pro (u-*) components only; see references/contract.md.
 */
import { ref, reactive } from 'vue'

const form = reactive({ name: '' })

function onBack() {}
function onSubmit() {}
</script>

<style lang="scss" scoped>
.page-stitch {
  min-height: 100vh;
  background: #f3f4f6;
}
</style>
