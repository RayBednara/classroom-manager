<template>
  <scoped-login />
</template>

<script>
export default {
  components: {
    ScopedLogin: () => import("@/components/scoped/login/TheLogin")
  }
}
</script>
