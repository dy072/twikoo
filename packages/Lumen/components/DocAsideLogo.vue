<script lang="ts">
import { defineComponent, PropType } from 'vue'

export default defineComponent({
  name: 'DocAsideLogo',
  props: {
    /**
     * `Aside_Data` 属性的类型定义。
     * 包含一个对象数组，每个对象代表一个横幅，具体字段如下：
     * - `link`: 链接地址
     * - `icon`: 图标地址
     * - `name` (可选): 名称
     * - `Activity` (可选): 活动信息
     * - `hide1` (可选): 隐藏信息1
     * - `info1` (可选): 信息1
     * - `hide2` (可选): 隐藏信息2
     * - `info2` (可选): 信息2
     *
     * 该属性为必需的。
     */
    Aside_Data: {
      type: Array as PropType<
        Array<{
          link: string
          icon: string
          name?: string
          Activity?: string
          hide1?: string
          info1?: string
          hide2?: string
          info2?: string
        }>
      >,
      required: true
    }
  }
})
</script>

<template>
  <div>
    <!-- 遍历 Aside_Data 数组并渲染 -->
    <a
      v-for="(banner, index) in Aside_Data"
      :key="index"
      :href="banner.link"
      :class="{ 'has-activity': banner.Activity, 'has-name': banner.name }"
      :title="banner.Activity || banner.name"
      class="banner"
      target="_blank"
      rel="noopener"
    >
      <img
        :src="banner.icon"
        width="22"
        height="22"
        :alt="banner.Activity || banner.name"
      />
      <span>
        <template v-if="banner.Activity">
          <p class="Activity" v-html="banner.Activity"></p>
        </template>
        <template v-if="banner.hide1 || banner.info1">
          <p v-if="banner.hide1" class="hide" v-html="banner.hide1"></p>
          <p v-if="banner.info1" class="info" v-html="banner.info1"></p>
        </template>
        <template v-if="banner.name">
          <p class="name" v-html="banner.name"></p>
        </template>
        <template v-if="banner.hide2 || banner.info2">
          <p v-if="banner.hide2" class="hide" v-html="banner.hide2"></p>
          <p v-if="banner.info2" class="info" v-html="banner.info2"></p>
        </template>
      </span>
    </a>
  </div>
</template>

<style lang="scss" scoped>
.banner {
  margin: 0.25rem 0;
  padding: 0.25rem 0;
  border-radius: 0.8rem;
  position: relative;
  font-size: 0.9rem;
  font-weight: 900;
  line-height: 1.1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  background-color: var(--vp-c-bg-alt);
  border: 1.5px solid var(--vp-c-bg-alt);
  transition: border-color 0.5s;

  &:last-of-type {
    margin-bottom: 1rem;
  }

  &:hover {
    img {
      transform: scale(1.75);
    }

    .hide {
      opacity: 0.9;
    }

    &.has-activity {
      border-color: rgba(100, 108, 255, 1);
    }

    &.has-name {
      border-color: var(--vp-c-brand-1);
    }
  }

  img {
    transition: transform 0.5s;
    transform: scale(1.25);
  }

  .hide {
    color: var(--vp-c-text-2);
    opacity: 0;
    font-size: 0.7rem;
    padding-left: 0.1rem;
    transition: opacity 0.5s;
  }

  .info {
    color: var(--vp-c-text-2);
    font-size: 0.7rem;
    padding-left: 0.1rem;
  }

  .name {
    background-image: linear-gradient(
      292deg,
      var(--vp-c-brand-3) 16%,
      var(--vp-c-brand-2),
      var(--vp-c-brand-1)
    );
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .Activity {
    background-image: linear-gradient(
      292deg,
      rgba(176, 71, 255, 1) 16%,
      rgba(100, 108, 255, 1),
      rgba(116, 123, 255, 1)
    );
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
}
</style>
