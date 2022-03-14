<template>
  <div class="dropdown container-menu">
    <div v-if="store.state.user.role === 'admin'">
      <div>
        <button
          class="btn btn-dark dropdown-toggle"
          type="button"
          id="dropdownMenuButton"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <img
            :src="store.state.user.image"
            alt="Profile"
            height="40"
            width="40"
            style="border-radius: 50%"
          />
        </button>
        <div
          class="dropdown-menu bg-secondary"
          aria-labelledby="dropdownMenuButton"
        >
          <button
            @click="router.push('/add-film')"
            class="dropdown-item bg-secondary text-light"
          >
            Add Film
          </button>
          <button
            @click="router.push('/all-films')"
            class="dropdown-item bg-secondary text-light"
          >
            All Films
          </button>
          <button
            @click="router.push('/categories')"
            class="dropdown-item bg-secondary text-light"
          >
            Categories
          </button>
          <button
            @click="router.push('/transactions')"
            class="dropdown-item bg-secondary text-light"
          >
            Transactions
          </button>
          <div class="dropdown-divider"></div>
          <button
            @click="router.push('/about')"
            class="dropdown-item bg-secondary text-light"
          >
            About Us
          </button>
          <button
            @click="handleLogout"
            class="dropdown-item bg-secondary text-light"
          >
            Logout
          </button>
        </div>
      </div>
    </div>
    <div v-else>
      <div>
        <button
          class="btn btn-dark dropdown-toggle"
          type="button"
          id="dropdownMenuButton"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <img
            :src="store.state.user.image"
            alt="Profile"
            height="40"
            width="40"
            style="border-radius: 50%"
          />
        </button>
        <div
          class="dropdown-menu bg-secondary"
          aria-labelledby="dropdownMenuButton"
        >
          <button
            @click="router.push('/profile')"
            class="dropdown-item bg-secondary text-light"
          >
            Profile
          </button>
          <button
            @click="router.push('/my-list')"
            class="dropdown-item bg-secondary text-light"
          >
            My List Film
          </button>
          <div class="dropdown-divider"></div>
          <button
            @click="router.push('/about')"
            class="dropdown-item bg-secondary text-light"
          >
            About Us
          </button>
          <button
            @click="handleLogout"
            class="dropdown-item bg-secondary text-light"
          >
            Logout
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useStore } from "vuex";
import { useRouter } from "vue-router";

export default {
  name: "MenuComponent",
  setup() {
    const store = useStore();
    const router = useRouter();

    const handleLogout = () => {
      store.commit("LOGOUT_USER");
      router.push("/");
    };

    return {
      store,
      handleLogout,
      router,
    };
  },
};
</script>

<style>
.container-menu {
  margin-top: 15px;
  margin-right: 15px;
}
</style>
