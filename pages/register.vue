<script setup>
const { $swal } = useNuxtApp();
// 表單格式
const userRegisteObject = ref({
  nickname: "",
  email: "",
  password: "",
  phone: "",
  birthday: "",
  address: {
    zipcode: "",
    detail: "",
  },
});

const processRegistration = async (requestBody) => {
  try {
    const response = await $fetch("/v1/user/signup", {
      method: "POST",
      body: {
        ...requestBody,
      },
      baseURL: "https://nuxr3.zeabur.app/api",
    });
    // 使用 sweetAlert2 套件顯示訊息
    await $swal.fire({
      position: "center",
      icon: "success",
      title: "註冊成功",
      showConfirmButton: false,
      timer: 1500,
    });
  } catch (error) {
    const { message } = error.response._data;
    await $swal.fire({
      position: "center",
      icon: "error",
      title: message,
      showConfirmButton: false,
      timer:5500,
    });
  } finally {
    userRegisteObject.value = { address: {} };
  }
};
</script>

<template>
  <div class="bg-light py-3 py-md-5 vh-100">
    <div class="container">
      <div class="row justify-content-md-center">
        <div class="col-12 col-md-11 col-lg-8 col-xl-7 col-xxl-6">
          <div class="bg-white p-4 p-md-5 rounded shadow-sm">
            <h2 class="h3 mb-4">會員註冊</h2>
            <form @submit.prevent="processRegistration(userRegisteObject)">
              <div class="form-floating mb-4">
                <input
                  type="text"
                  class="form-control"
                  id="firstName"
                  placeholder="王小明"
                  required
                  v-model="userRegisteObject.name"
                />
                <label for="firstName"
                  >姓名 <span class="text-danger">*</span></label
                >
              </div>

              <div class="form-floating mb-4">
                <input
                  type="email"
                  class="form-control"
                  id="email"
                  placeholder="example@gmail.com"
                  pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
                  required
                  v-model="userRegisteObject.email"
                />
                <label for="email"
                  >信箱 <span class="text-danger">*</span></label
                >
              </div>

              <div class="form-floating mb-4">
                <input
                  type="password"
                  class="form-control"
                  id="password"
                  placeholder="請輸入 8 碼以上密碼"
                  pattern=".{8,}"
                  required
                  v-model="userRegisteObject.password"
                />
                <label for="password"
                  >密碼 <span class="text-danger">*</span></label
                >
              </div>

              <div class="form-floating mb-4">
                <input
                  type="tel"
                  class="form-control"
                  id="phone"
                  placeholder="0912345678"
                  pattern="(\+886|0)?9\d{8}|(\+886|0)?2\d{8}|\d{3}-\d{4}-\d{4}"
                  required
                  v-model="userRegisteObject.phone"
                />
                <label for="phone">電話</label>
              </div>

              <div class="form-floating mb-4">
                <input
                  type="date"
                  class="form-control"
                  id="dateInput"
                  required
                  v-model="userRegisteObject.birthday"
                />
                <label for="dateInput">出生年月日</label>
              </div>

              <div class="row">
                <div class="col-md-6">
                  <div class="form-floating mb-4">
                    <input
                      type="text"
                      class="form-control"
                      id="zipcode"
                      placeholder="100"
                      pattern="\d{3,}"
                      required
                      v-model="userRegisteObject.address.zipcode"
                    />
                    <label for="zipcode">郵遞區號</label>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="form-floating mb-4">
                    <input
                      type="text"
                      class="form-control"
                      id="address"
                      placeholder="台北市中正區重慶南路一段"
                      required
                      v-model="userRegisteObject.address.detail"
                    />
                    <label for="address">詳細地址</label>
                  </div>
                </div>
              </div>

              <button class="btn btn-lg btn-primary w-100" type="submit">
                註冊
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
