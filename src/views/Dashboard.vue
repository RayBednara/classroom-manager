<template>
  <div>This is dashboard page.</div>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: false
    };
  },
  created() {
    try {
      console.log("Logged in.");
      const user = JSON.parse(localStorage.getItem("classroom.user"));
      console.log(user);
    } catch (er) {
      console.error(er);
    }
  }
};
</script>
