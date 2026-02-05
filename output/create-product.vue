<template>
  <view class="page-create-product">
    <u-navbar title="创建商品" :autoBack="true" placeholder border />

    <view class="tabs-wrap">
      <u-tabs
        :list="tabList"
        :current="tabCurrent"
        active-color="#1677FF"
        inactive-color="#606266"
        @change="onTabChange"
      />
    </view>

    <view class="content">
      <u-card title="基本信息" :padding="32">
        <u-form :model="form" ref="uForm">
          <u-form-item label="商品分类" prop="category" required borderBottom>
            <u-input
              v-model="form.categoryText"
              type="select"
              placeholder="请选择分类"
              :select-open="showCategoryPicker"
              border="none"
              @click="showCategoryPicker = true"
            />
            <u-picker
              v-model="showCategoryPicker"
              mode="selector"
              :range="categoryOptions"
              @confirm="onCategoryConfirm"
            />
          </u-form-item>
          <u-form-item label="商品名称" prop="name" required borderBottom>
            <u-input v-model="form.name" placeholder="请输入商品名称 (20字以内)" border="none" />
          </u-form-item>
          <u-form-item borderBottom>
            <template #label>
              <text>商品副标题</text>
              <u-text text=" (选填)" type="info" size="24" />
            </template>
            <u-input v-model="form.subtitle" placeholder="请输入卖点描述，如：限时优惠" border="none" />
          </u-form-item>
          <u-form-item label="商品主图" prop="images" required borderBottom>
            <u-upload
              :fileList="fileList"
              @afterRead="afterRead"
              @delete="onDeletePic"
              :maxCount="5"
            />
            <view class="upload-tips">
              <u-text text="建议尺寸 375x375，最多上传 5 张" type="info" size="24" block />
              <u-text text="默认第一张图为主图封面" type="warning" size="24" block />
            </view>
          </u-form-item>
          <u-form-item label="上架状态" prop="onSale" borderBottom>
            <u-switch v-model="form.onSale" activeColor="#1677FF" />
          </u-form-item>
          <u-collapse>
            <u-collapse-item title="更多品牌信息">
              <u-form-item label="品牌/系列" prop="brand" borderBottom>
                <u-input
                  v-model="form.brandText"
                  type="select"
                  placeholder="请选择品牌"
                  :select-open="showBrandPicker"
                  border="none"
                  @click="showBrandPicker = true"
                />
                <u-picker
                  v-model="showBrandPicker"
                  mode="selector"
                  :range="brandOptions"
                  @confirm="onBrandConfirm"
                />
              </u-form-item>
            </u-collapse-item>
          </u-collapse>
        </u-form>
      </u-card>

      <u-card :padding="32">
        <u-section title="销售与规格">
          <template #right>
            <view class="section-right-row">
              <u-text text="多规格模式" type="info" size="24" />
              <u-switch v-model="form.multiSpec" activeColor="#1677FF" size="small" />
            </view>
          </template>
        </u-section>
        <u-form :model="form" ref="formSale">
          <u-form-item label="销售方式" prop="salesMethod" borderBottom>
            <u-radio-group v-model="form.salesMethod">
              <u-radio label="商城销售" value="mall" />
              <u-radio label="积分商城" value="points" />
              <u-radio label="两个都支持" value="both" />
            </u-radio-group>
          </u-form-item>
          <u-form-item label="销售价(元)" prop="price" required borderBottom>
            <u-number-box v-model="form.price" :min="0" :step="0.01" />
          </u-form-item>
          <u-form-item label="成本价(元)" prop="cost" required borderBottom>
            <u-number-box v-model="form.cost" :min="0" :step="0.01" />
          </u-form-item>
          <u-form-item label="库存" prop="stock" required borderBottom>
            <u-number-box v-model="form.stock" :min="0" :step="1" />
          </u-form-item>
          <u-form-item label="分佣基数" borderBottom>
            <view class="commission-content">
              <u-radio-group v-model="form.commissionBaseType">
                <u-radio label="设定固定值" value="fixed" />
                <u-radio label="根据成本价动态生成" value="dynamic" />
              </u-radio-group>
              <view class="input-with-unit">
                <u-number-box v-model="form.commissionBase" :min="0" :step="0.01" />
                <u-text text="元" type="info" size="28" />
              </view>
            </view>
          </u-form-item>
          <u-row gutter="20">
            <u-col span="6">
              <u-form-item label="起售数量" prop="minBuy" required borderBottom>
                <u-input v-model="form.minBuy" type="number" placeholder="1" border="none" />
              </u-form-item>
            </u-col>
            <u-col span="6">
          <u-form-item borderBottom>
            <template #label>
              <text>虚拟销量</text>
              <u-text text=" (前端显示)" type="info" size="24" />
            </template>
                <u-input v-model="form.fakeSales" type="number" placeholder="0" border="none" />
              </u-form-item>
            </u-col>
          </u-row>
        </u-form>
      </u-card>

      <u-card title="服务与预约" :padding="32">
        <u-row gutter="20">
          <u-col span="6">
            <u-form-item label="服务时长(分钟)" prop="duration" required borderBottom>
              <u-input v-model="form.duration" type="number" placeholder="例如: 60" border="none" />
            </u-form-item>
          </u-col>
          <u-col span="6">
            <u-form-item label="有效期天数" prop="validity" required borderBottom>
              <u-input
                v-model="form.validityText"
                type="select"
                placeholder="永久有效"
                :select-open="showValidityPicker"
                border="none"
                @click="showValidityPicker = true"
              />
              <u-picker
                v-model="showValidityPicker"
                mode="selector"
                :range="validityOptions"
                @confirm="onValidityConfirm"
              />
            </u-form-item>
          </u-col>
        </u-row>
      </u-card>

      <u-card title="规则设置" :padding="32">
        <u-form :model="form">
          <u-form-item borderBottom>
            <template #label>
              <text>每人限购</text>
              <u-text text=" (0为不限)" type="info" size="24" />
            </template>
            <u-input v-model="form.limitPerUser" type="number" placeholder="请输入限购数量" border="none" />
          </u-form-item>
          <u-form-item label="退款规则" prop="refundRule" required borderBottom>
          <u-input
            v-model="form.refundRuleText"
            type="select"
            placeholder="随时退 (无条件退款)"
            :select-open="showRefundPicker"
            border="none"
            @click="showRefundPicker = true"
          />
          <u-picker
            v-model="showRefundPicker"
            mode="selector"
            :range="refundOptions"
            @confirm="onRefundConfirm"
          />
        </u-form-item>
        </u-form>
      </u-card>

      <u-card title="图文详情" :padding="32">
        <view class="rich-area">
          <u-textarea
            v-model="form.detail"
            placeholder="可输入服务特色、环境描述等"
            :maxlength="-1"
            count
          />
          <u-line color="#e5e7eb" margin="0" />
          <view class="rich-toolbar">
            <u-button type="primary" icon="photo" text="插入图片" @click="onInsertImage" />
          </view>
        </view>
      </u-card>
    </view>

    <u-toast ref="uToast" />
  </view>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'

const tabList = [
  { name: '服务商品' },
  { name: '到店商品' },
  { name: '快递商品' },
]
const tabCurrent = ref(1)

const categoryOptions = ['请选择分类', '美容美发', '休闲娱乐', '餐饮美食']
const brandOptions = ['请选择品牌', '自有品牌', '合作品牌']
const validityOptions = ['永久有效', '购买后30天', '购买后90天']
const refundOptions = ['随时退 (无条件退款)', '不可退 (特殊商品)', '过期自动退']

const showCategoryPicker = ref(false)
const showBrandPicker = ref(false)
const showValidityPicker = ref(false)
const showRefundPicker = ref(false)

const fileList = ref<Array<{ url: string }>>([])

const form = reactive({
  categoryText: '',
  category: 0,
  name: '',
  subtitle: '',
  onSale: true,
  brandText: '',
  brand: 0,
  salesMethod: 'mall',
  price: 0,
  cost: 0,
  stock: 0,
  multiSpec: false,
  commissionBaseType: 'fixed',
  commissionBase: 0,
  minBuy: 1,
  fakeSales: 0,
  duration: '',
  validityText: '永久有效',
  validity: 0,
  limitPerUser: '',
  refundRuleText: '随时退 (无条件退款)',
  refundRule: 0,
  detail: '',
})

function onTabChange(index: number) {
  tabCurrent.value = index
}

function onCategoryConfirm(e: { value?: number[]; [k: string]: unknown }) {
  const idx = Array.isArray(e?.value) ? e.value[0] : (e as number[])?.[0]
  if (idx != null) {
    form.category = idx
    form.categoryText = categoryOptions[idx]
  }
  showCategoryPicker.value = false
}

function onBrandConfirm(e: { value?: number[]; [k: string]: unknown }) {
  const idx = Array.isArray(e?.value) ? e.value[0] : (e as number[])?.[0]
  if (idx != null) {
    form.brand = idx
    form.brandText = brandOptions[idx]
  }
  showBrandPicker.value = false
}

function onValidityConfirm(e: { value?: number[]; [k: string]: unknown }) {
  const idx = Array.isArray(e?.value) ? e.value[0] : (e as number[])?.[0]
  if (idx != null) {
    form.validity = idx
    form.validityText = validityOptions[idx]
  }
  showValidityPicker.value = false
}

function onRefundConfirm(e: { value?: number[]; [k: string]: unknown }) {
  const idx = Array.isArray(e?.value) ? e.value[0] : (e as number[])?.[0]
  if (idx != null) {
    form.refundRule = idx
    form.refundRuleText = refundOptions[idx]
  }
  showRefundPicker.value = false
}

function afterRead() {}

function onDeletePic() {}

function onInsertImage() {
  uni.$u.toast('插入图片')
}
</script>

<style lang="scss" scoped>
.page-create-product {
  min-height: 100vh;
  background: #f5f6fa;
}

.tabs-wrap {
  background: #fff;
  border-bottom: 1rpx solid #e5e7eb;
}

.content {
  padding: 32rpx;
  display: flex;
  flex-direction: column;
  gap: 32rpx;
}

/* u-section 右侧插槽：多规格模式一行 */
.section-right-row {
  display: flex;
  align-items: center;
  gap: 16rpx;
}

/* 上传说明：使用 u-text 后仅保留间距 */
.upload-tips {
  margin-top: 16rpx;
  display: flex;
  flex-direction: column;
  gap: 8rpx;
}

/* 分佣基数：单选 + 金额输入 */
.commission-content {
  display: flex;
  flex-direction: column;
  gap: 24rpx;
}
.input-with-unit {
  display: flex;
  align-items: center;
  gap: 16rpx;
}

.rich-area {
  border: 1rpx solid #e5e7eb;
  border-radius: 20rpx;
  overflow: hidden;
  min-height: 420rpx;
}
.rich-toolbar {
  padding: 24rpx;
  background: #f3f4f6;
}
</style>
