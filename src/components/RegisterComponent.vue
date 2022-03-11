<template>
  <div>
    <div v-if="validation" class="text-danger">
      {{ validation.message }}
    </div>
    <h2>Register</h2>
    <form @submit.prevent="handleOnSubmit">
      <div>
        <input
          className="form-auth-input"
          type="text"
          name="fullName"
          v-model="form.fullName"
          id="fullName"
          placeholder="Name"
        />
      </div>
      <div>
        <input
          className="form-auth-input"
          type="email"
          name="email"
          v-model="form.email"
          id="email"
          placeholder="Email"
        />
      </div>
      <div>
        <input
          className="form-auth-input"
          type="text"
          name="phone"
          v-model="form.phone"
          id="phone"
          placeholder="Phone Number"
        />
      </div>
      <div>
        <input
          className="form-auth-input"
          type="password"
          name="password"
          v-model="form.password"
          id="password"
          placeholder="Password"
        />
      </div>
      <button type="submit" className="form-auth-button">Register</button>
    </form>
  </div>
</template>

<script>
import { API } from "@/config/api";
import { reactive, ref } from "vue";
import Swal from "sweetalert2";

export default {
  name: "RegisterComponent",
  setup() {
    const form = reactive({
      fullName: "",
      phone: "",
      email: "",
      password: "",
    });

    const validation = ref([]);

    const handleOnSubmit = async () => {
      try {
        const config = {
          headers: {
            "Content-type": "application/json",
          },
        };

        const body = JSON.stringify(form);

        await API.post("/register", body, config);

        form.fullName = "";
        form.phone = "";
        form.email = "";
        form.password = "";

        Swal.fire("Good job!", "Registration Success, please login", "success");
      } catch (error) {
        validation.value = error.response.data;
        console.log(error);
      }
    };

    return {
      form,
      validation,
      handleOnSubmit,
    };
  },
};
</script>

<style></style>
