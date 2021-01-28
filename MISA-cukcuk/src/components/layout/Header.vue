<template>
  <div class="header">
    <div class="department-info">
      <select>
        <option v-for="(item, index) in departments" :key="index">
          {{ item }}
        </option>
      </select>
    </div>
    <div class="account-info">
      <div class="account-avatar"></div>
      <div class="account-name">Đồng Minh Cường</div>
      <div class="account-option icon-option-default-16"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    departments: {
      type: Array,
      default: () => [],
    },
  },
};
</script>