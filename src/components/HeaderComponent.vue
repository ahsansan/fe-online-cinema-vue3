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
        <router-link class="link-menu-class" to="/about">About</router-link>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderComponent",
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
