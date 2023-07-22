<template>
  <!-- <button type="button" :class="classes" @click="onClick" :style="style">{{ label }} </button> -->
  <button type="button" :class="classes">{{ label }}</button>
</template>

<script lang="ts" setup>
import { computed } from 'vue';
import colors from '../../style/colors';

const props = withDefaults(defineProps<{
  /**
   * The label of the button
   */
  label: string,
  /**
   * primary or secondary button
   */
  primary?: boolean,
  /**
   * size of the button
   */
  size?: 'small' | 'medium' | 'large',
  /**
   * corner rounded of the button
   */
  rounded?: boolean,
  /**
   * style of the button
   */
  variant?: 'plained' | 'outlined'
  /**
   * shadow
   */
  shadow?: boolean

}>(), { primary: true, size: 'medium', rounded: false, variant: 'plained', shadow: false });

const emit = defineEmits<{
  (e: 'click', id: number): void;
}>();

const classes = computed(() => ({
  'bg-red-200': true,
  'px-2 py-1': true,
  'text-sm': props.size ==='small',
  'text-base': props.size ==='medium',
  'text-lg': props.size ==='large',
  'rounded': props.rounded,
  [`bg-emerald-600 text-emerald-100`]: props.primary === true && props.variant === 'plained',
  [`bg-zinc-900 text-zinc-100`]: props.primary === false && props.variant === 'plained',
  [`bg-zinc-100 text-emerald-600 ring-1 ring-inset ring-emerald-600`]: props.primary === true && props.variant === 'outlined',
  [`bg-zinc-100 text-zinc-900 ring-1 ring-inset ring-zinc-900`]: props.primary === false && props.variant === 'outlined',
  [`shadow-md`]: props.shadow,
}));

const onClick = () => {
  emit("click", 1)
};

</script>