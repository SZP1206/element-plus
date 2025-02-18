<template>
  <el-popper
    v-model:visible="visible"
    :trigger="['click']"
    effect="light"
    pure
  >
    <div class="el-popconfirm">
      <p class="el-popconfirm__main">
        <i
          v-if="!hideIcon"
          :class="icon"
          class="el-popconfirm__icon"
          :style="{color: iconColor}"
        ></i>
        {{ title }}
      </p>
      <div class="el-popconfirm__action">
        <el-button
          size="mini"
          :type="cancelButtonType"
          @click="cancel"
        >
          {{ cancelButtonText }}
        </el-button>
        <el-button
          size="mini"
          :type="confirmButtonType"
          @click="confirm"
        >
          {{ confirmButtonText }}
        </el-button>
      </div>
    </div>
    <template #trigger>
      <slot name="reference"></slot>
    </template>
  </el-popper>
</template>

<script lang="ts">
import { defineComponent,ref } from 'vue'
import { Button as ElButton } from '@element-plus/button'
import { Popper as ElPopper } from '@element-plus/popper'
import { t } from '../../locale'

export default defineComponent({
  name: 'ElPopconfirm',

  components: {
    ElButton,
    ElPopper,
  },

  props: {
    title: {
      type: String,
    },
    confirmButtonText: {
      type: String,
      default: t('el.popconfirm.confirmButtonText'),
    },
    cancelButtonText: {
      type: String,
      default: t('el.popconfirm.cancelButtonText'),
    },
    confirmButtonType: {
      type: String,
      default: 'primary',
    },
    cancelButtonType: {
      type: String,
      default: 'text',
    },
    icon: {
      type: String,
      default: 'el-icon-question',
    },
    iconColor: {
      type: String,
      default: '#f90',
    },
    hideIcon: {
      type: Boolean,
      default: false,
    },
  },
  emits:['confirm','cancel'],
  setup(props,{ emit }){
    const visible = ref(false)
    const confirm = () => {
      visible.value = false
      emit('confirm')
    }
    const cancel = () => {
      visible.value = false
      emit('cancel')
    }

    return {
      visible,
      confirm,
      cancel,
    }
  },
})
</script>
