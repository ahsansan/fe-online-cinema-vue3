<template>
  <div class="container-header" fluid>
    <div>
      <router-link to="/"
        ><img
          class="logo-class"
          src="@/assets/OnlineCinemaIcon.png"
          alt="Online Cinema"
      /></router-link>
    </div>
    <div>
      <nav>
        <div v-if="store.state.isLogin === true">
          <router-link class="link-menu-class" to="/about">About</router-link> |
          <button @click="handleLogout" class="link-menu-class">Logout</button>
        </div>
        <div v-else>
          <router-link class="link-menu-class" to="/about">About</router-link> |
          <router-link class="link-menu-class" to="/auth">Auth</router-link>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
import { useStore } from "vuex";
export default {
  name: "HeaderComponent",
  setup() {
    const store = useStore();

    const handleLogout = () => {
      store.commit("LOGOUT_USER");
    };

    return {
      store,
      handleLogout,
    };
  },
};
</script>

<style>
.container-header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  background: #000;
  height: 12vh;
}
.logo-class {
  padding: 20px;
}
.link-menu-class {
  background-color: orange;
  color: #000;
  padding: 10px;
  text-decoration: none;
  border-radius: 5px;
}
.link-menu-class:hover {
  background-color: rgb(255, 221, 159);
  color: #000;
}
</style>
