<template>
  <Menubar :model="menuItems">
    <template #end>
      <h1 class="text-green-600 text-2xl font-normal m-0 p-0">
        Vue Js Music recommendation App
      </h1>
    </template>
  </Menubar>
</template>

<script>
import {useUserStore} from "../stores/UserStore.js";

export default {
  data() {
    return {
      userStore: useUserStore(),
      username:""
    };
  },
  computed: {

    isUserLoggedIn() {
      /*this.userStore.userId !== "";*/
      var userId = localStorage.getItem("user");
      return userId !== null;
    },
    menuItems() {
      const localStorageData = localStorage.getItem("user");
      const parsedLocalStorageData = JSON.parse(localStorageData);
      parsedLocalStorageData?this.username = parsedLocalStorageData.username:this.username = "";
      const baseItems = [
        {
          label: "Home",
          icon: "pi pi-home",
          to: "/",
        },
        {
          label: this.isUserLoggedIn ? this.username: "Profile",
          icon: "pi pi-user",
          to: "/profile",
        },

      ];

      const authItems = [
        {
          label: "Auth",
          icon: "pi pi-sign-in",
          to: "/auth",
        },
        {
          label: "Register",
          icon: "pi pi-sign-in",
          to: "/register",
        },
      ];

      return this.isUserLoggedIn ? baseItems : authItems;
    },
  },
};
</script>

<style scoped></style>
