<script setup>
import { watchEffect } from 'vue'

var userState = null

if (process.client) {
  userState = useUserState()
  const accountType = useAccountType();
  const accountTypeList = useAccountTypeList();
  const userLoginState = computed(() => accountTypeList.value.find(i => i.title == accountType.value) && userState.value)
  watchEffect(() => {
    if (!userLoginState.value) {
      navigateTo("/home")
    }
  })
}
</script>
<template>
  <div v-show="userState" class="wrapper">
    <NuxtLink to="/user">User</NuxtLink>
    <NuxtLink to="/logout">Logout</NuxtLink>
    <slot />
  </div>
</template>
<style lang="scss" scoped>
.wrapper {
  @apply text-center my-12;
}
a {
  @apply px-4;

  &.router-link-active {
    @apply bg-gray-200;
  }
}
</style>