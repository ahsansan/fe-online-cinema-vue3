<template>
  <div class="container-detail" fluid>
    <div class="container-detail-tumbnail">
      <img :src="film.tumbnail" alt="{{film.title}}" class="detail-tumbnail" />
    </div>
    <div class="container-detail">
      <h2>{{ film.title }}</h2>
      <h4 class="detail-genre">{{ film.category?.name }}</h4>
      <p class="detail-harga">
        {{ convertToRupiah(199000) }} -- {{ film.price }}
      </p>
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
import axios from "axios";
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";

export default {
  name: "Detail",
  setup() {
    const route = useRoute();
    let film = ref({});

    onMounted(() => {
      const id = route.params.id;
      axios
        .get(`http://localhost:5000/api/cinema/v1/film/${id}`)
        .then((result) => {
          film.value = result.data.data.film;
        })
        .catch((err) => {
          console.log(err.response);
        });
    });

    return {
      film,
    };
  },
  methods: {
    convertToRupiah(angka) {
      let rupiah = "";
      const angkarev = angka.toString().split("").reverse().join("");
      for (var i = 0; i < angkarev.length; i++) {
        if (i % 3 === 0) rupiah += angkarev.substr(i, 3) + ".";
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
  background-color: black;
  color: white;
  padding-top: 25px;
  padding-bottom: 25px;
  min-height: 70vh;
}
.detail-tumbnail {
  border-radius: 5px;
}
</style>
