<template>
  <div class="m-auto wrapper">
    <div class="card-container container">
      <div class="m-auto col-4 rounded-2 text-light flip-card">
        <div class="flip-card-inner bg-success">
          <div class="row logo m-auto">
            <div class="logo col-4 ms-2">
              <img
                src="../assets/2_2_paracard_933x575.jpg"
                alt=""
                class="w-100"
              />
            </div>
          </div>
          <div class="p-0">
            <div class="chip col-2 mt-1 ms-3">
              <img src="../assets/chip.png" alt="" class="w-75" />
            </div>

            <div class="mt-1 ms-3">
              <h3>{{ number }}</h3>
            </div>
            <div class="row master-logo me-1">
              <div class="d-flex align-items-end flex-column mb-2">
                <img src="../assets/Mastercard-logo.png" />
              </div>
            </div>
            <div class="row detail m-auto">
              <div class="col ms-3">
                <div class="me-5">{{ name }}</div>
              </div>
              <div class="col text-end me-2">
                <div>Valid Thru: {{ date }}</div>
              </div>
            </div>
          </div>
          <div class="flip-card-back bg-success rounded-2">
            <div class="p-4 bg-dark mt-5"></div>

            <div class="cvv mt-4 p-2 bg-light w-50 m-auto">
              <span class="text-dark"
                >CVV <span class="ms-2">{{ cvv }}</span></span
              >
            </div>
          </div>
        </div>
      </div>
      <form class="m-auto col-5 mt-2">
        <input
          class="form-control mb-2"
          :value="formatCardNumber"
          @input="updateValue"
          maxlength="19"
          placeholder="Enter your card number"
        />
        <div class="error" v-if="!$v.cardNumber.numeric">
          Kart numarası harf içeremez
        </div>
        <div class="row">
          <div class="col">
            <input
              class="form-control mb-2"
              v-model="name"
              placeholder="Enter your name"
              type="text"
            />
          </div>
          <div class="col">
            <input class="form-control mb-2" type="month" v-model="date" />
          </div>
        </div>
        <input
          type="text"
          class="form-control mb-2"
          placeholder="CVV"
          maxlength="3"
          v-model="cvv"
        />
        <button type="submit" class="btn p-2 form-control border bg-light">
          Send
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import { numeric } from "vuelidate/lib/validators";

export default {
  name: "CreditCard",
  data() {
    return {
      date: "",
      name: "",
      cardNumber: "",
      number: "",
      cvv: "",
    };
  },
  computed: {
    formatCardNumber() {
      return this.cardNumber ? this.cardNumber.match(/.{1,4}/g).join(" ") : "";
    },
  },
  methods: {
    updateValue(e) {
      this.cardNumber = e.target.value.replace(/ /g, "");
      this.number = e.target.value.replace(/ /g, " ");
    },
  },
  validations: {
    cardNumber: {
      numeric,
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.flip-card-inner {
  position: relative;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
  backface-visibility: hidden;
}
.flip {
  transform: rotateY(180deg);
  backface-visibility: hidden;
}
.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}
.flip-card-back {
  color: white;
  transform: rotateY(180deg);
  position: absolute;
  top: 1px;
}
.wrapper {
  background-color: aliceblue;
  height: 100vh;
}
.card-container {
  padding-top: 100px;
}
.logo,
.detail {
  background-color: #fff;
  color: black;
}
.error {
  color: red;
}
.master-logo img {
  width: 15%;
}
</style>
