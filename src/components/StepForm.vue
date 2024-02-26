<script setup>
import { ref } from "vue";
const steps = ref({});
const step = ref(1);
const customer = ref({
  firstName: "",
  lastName: "",
  phoneNumber: "",
  address: "",
  country: "",
  city: "",
  birthDay: "",
  termOfService: "",
  pinCode: "",
  eMail: "",
});
const hasSeenCongrats = ref(false);
const tempCustomer = ref({
  gender: "",
  firstName: "",
  lastName: "",
  phoneNumber: "",
  address: "",
  zipCode: "",
  city: "",
  birthDay: "",
  termOfService: "",
  pinCode: "",
  eMail: "",
});

const next = (event) => {
  event.preventDefault();
  if (step.value > 2) {
    step.value = 3;
  } else {
    step.value++;
  }
};
const back = (event) => {
  event.preventDefault();
  if (step.value < 2) {
    step.value = 1;
  } else {
    step.value--;
  }
};
const customerRegister = () => {
  hasSeenCongrats.value = true;
  step.value = 4;
};
</script>

<template>
  <h1 class="text-4xl font-bold">Sign up form with multiple steps in VUE3</h1>
  <div class="flex justify-center items-center py-10">
    <div
      class="step"
      :class="{ 'step-active': step === 1, 'step-done': step > 1 }"
    >
      1
    </div>
    <div
      class="step"
      :class="{ 'step-active': step === 2, 'step-done': step > 2 }"
    >
      2
    </div>
    <div
      class="step"
      :class="{ 'step-active': step === 3, 'step-done': step > 3 }"
    >
      3
    </div>
  </div>
  <transition name="slide-fade">
    <section v-show="step === 1">
      <form
        class="form text-start"
        method="post"
        action="#"
        @submit.prevent="next"
      >
        <div class="form-group text-center">
          <input
            class="w-2/5"
            type="text"
            v-model="customer.firstName"
            autocomplete="customer.firstName"
            placeholder="姓氏"
            required
          />
          <input
            class="w-2/5"
            type="text"
            v-model="customer.lastName"
            autocomplete="customer.lastName"
            placeholder="名字"
            required
          />
        </div>
        <div class="form-group text-center">
          <div class="text-start pl-16 text-sm font-bold">出生年月日</div>
          <input
            class="w-10/12"
            v-model="customer.birthDay"
            autocomplete="customer.birthDay"
            type="date"
          />
        </div>
        <div class="text-center font-bold text-xl mt-5">
          <button class="no-outline" type="submit">下一步 &#x2192;</button>
        </div>
      </form>
    </section>
  </transition>
  <transition name="slide-fade">
    <section v-show="step === 2">
      <form class="form" method="post" action="#" @submit.prevent="next">
        <div class="form-group text-center">
          <input
            class="w-2/5"
            v-model="customer.country"
            autocomplete="customer.country"
            type="text"
            placeholder="國籍"
          />
          <input
            class="w-2/5"
            v-model="customer.city"
            autocomplete="customer.city"
            type="text"
            placeholder="縣市"
          />
        </div>
        <div class="form-group text-center">
          <input
            class="w-10/12"
            type="text"
            v-model="customer.address"
            autocomplete="customer.address"
            placeholder="詳細地址"
          />
        </div>
        <div class="flex justify-between font-bold text-xl mt-5 mx-20">
          <button class="no-outline" @click.prevent="back">
            &larr; 上一步
          </button>
          <button class="no-outline" type="submit">下一步 &#x2192;</button>
        </div>
      </form>
    </section>
  </transition>
  <transition name="slide-fade">
    <section v-show="step === 3">
      <form
        class="form"
        method="post"
        action="#"
        @submit.prevent="customerRegister"
      >
        <div class="form-group text-center">
          <input
            class="w-10/12"
            type="text"
            v-model="customer.phoneNumber"
            autocomplete="customer.phoneNumber"
            placeholder="手機號碼"
          />
        </div>
        <div class="form-group text-center">
          <input
            class="w-10/12"
            type="email"
            v-model="customer.eMail"
            autocomplete="customer.eMail"
            placeholder="電子信箱"
          />
        </div>
        <div class="flex justify-between font-bold text-xl mt-5 mx-20">
          <button class="no-outline" @click.prevent="back">
            &larr; 上一步
          </button>
          <button class="no-outline" type="submit">完成 &#x2192;</button>
        </div>
      </form>
    </section>
  </transition>
  <!-- 填完表單後 -->
  <section class="bg-black" v-if="hasSeenCongrats">
    <div class="text-4xl font-bold text-white py-5">
      感謝您的填寫！&#128538;
    </div>
  </section>
</template>

<style scoped>
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.slide-fade-enter,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateX(10px);
}

/* 步驟樣式 */
.step {
  background-color: rgb(175, 175, 175);
  color: aliceblue;
  margin: 0 90px;
  padding: 10px 17px;
  border-radius: 50%;
  position: relative;
}
.step::before {
  content: "";
  position: absolute;
  height: 6px;
  width: 183px;
  background-color: rgb(175, 175, 175);
  top: 50%;
  left: -181px;
  z-index: -1;
}
.step:first-child::before {
  content: none;
}

.step-active,
.step-done {
  background-color: black;
}

.step-active.step::before,
.step-done.step::before {
  background-color: black;
}
/* 表單樣式 */
.form-group {
  input {
    padding: 10px 20px;
    margin: 10px 10px 50px 10px;
    border-radius: 5px;
    border: 1px solid #cecece;
  }
}
.no-outline {
  border: none;
  outline: none;
  background: none;
  cursor: pointer;
  padding: 0;
  margin: 0;
  color: #828282;
}

.no-outline:hover {
  text-decoration: none;
  color: #000000;
  font-weight: bold;
}
</style>
