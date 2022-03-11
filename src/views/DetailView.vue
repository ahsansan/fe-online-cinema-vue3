<template>
  <div class="container-detail" fluid>
    <div></div>
    <div class="container-detail-tumbnail">
      <img :src="film.tumbnail" alt="{{film.title}}" class="detail-tumbnail" />
    </div>
    <div class="container-detail">
      <h2>{{ film.title }}</h2>
      <div v-if="trans.status === 'Approved'"></div>
      <div v-else>
        <div>
          <div v-if="store.state.isLogin === true">
            <div v-if="store.state.user.role === 'admin'">
              <button>Edit Film</button>
            </div>
            <div v-else>
              <button v-b-modal.modal-purchase>Buy Film</button>
            </div>
          </div>
          <div v-else>
            <button @click="beforeLogin">Buy Film</button>
          </div>
          <b-modal id="modal-purchase" :title="film.title">
            <p class="my-4">Modal Purchase</p>
          </b-modal>
        </div>
      </div>
      <h4 class="detail-genre">{{ film.category?.name }}</h4>
      <div v-if="trans.status === 'Approved'"></div>
      <div v-else>
        {{ convertToRupiah(film.price) }}
      </div>
      <p className="detail-desk">{{ film.description }}</p>
      <iframe
        :src="film.filmUrl"
        :title="film.title"
        frameBorder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowFullScreen
      ></iframe>
    </div>
  </div>
</template>

<script>
import { API } from "@/config/api";
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import { useStore } from "vuex";
import { useRouter } from "vue-router";

export default {
  name: "Detail",
  setup() {
    const route = useRoute();
    let film = ref({});
    let trans = ref({});
    const store = useStore();
    const router = useRouter();

    const beforeLogin = () => {
      router.push("/auth");
    };

    onMounted(async () => {
      try {
        const resp = await API.get(`/film/${route.params.id}`);

        film.value = resp.data.data.film;
      } catch (err) {
        console.log(err.response);
      }
    });

    onMounted(async () => {
      try {
        const resp = await API.get(`/transaction/${route.params.id}`);

        trans.value = resp.data.data;
      } catch (err) {
        console.log(err.response);
      }
    });

    return {
      film,
      trans,
      store,
      beforeLogin,
    };
  },
  methods: {
    convertToRupiah(angka) {
      let rupiah = "";
      if (angka) {
        const angkarev = angka.toString().split("").reverse().join("");
        for (var i = 0; i < angkarev.length; i++) {
          if (i % 3 === 0) rupiah += angkarev.substr(i, 3) + ".";
        }
      }

      return (
        "Rp. " +
        rupiah
          .split("", rupiah.length - 1)
          .reverse()
          .join("")
      );
    },
  },
};
</script>

<style>
.container-detail {
  color: white;
  padding-top: 25px;
  padding-bottom: 25px;
  min-height: 70vh;
}
.detail-tumbnail {
  border-radius: 5px;
}
</style>
