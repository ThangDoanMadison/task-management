<script>
import SideBar from "@/components/sidebar/SideBar";
import { sidebarWidth } from "@/components/sidebar/state";
export default {
  components: { SideBar },
  setup() {
    return { sidebarWidth };
  },
};
</script>
<template>
  <SideBar />
  <div :style="{ 'margin-left': sidebarWidth }">
    <router-view />
  </div>
</template>

<style>
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
