<script setup>
navigateTo("/register");
</script>

<template>
  <div>Page: index</div>
</template>

<style scoped></style>
// 在 /pages/register.vue 使用模板提供的操作介面填寫註冊表單。點擊 “註冊” 按鈕後使用 Nuxt3 提供的方法串接旅館的 註冊 API ，將請求送出。
//https://todolist-api.hexschool.io/users/sign_up

// 需使用 try catch 處理請求成功與失敗的訊息，請求成功與失敗皆使用 sweetAlert2 套件 顯示訊息。sweetAlert2 套件在模板已有安裝與引入，不需再額外設定。
// $swal.fire({
//   position: "center",
//   icon: ... ,
//   title: ... ,
//   showConfirmButton: false,
//   timer: 1500,
// });
// 表單不需處理表單驗證、身分驗證、檢查登入狀態以及存入 cookie。
// 註冊 API 夾帶的請求體（Request Body）格式，需要注意以下地方 :
// 所有欄位都必填。
// 密碼需要至少 8 碼以上，並英數混合。
// 電話格式可以是手機號碼與市內電話。
// birthday 格式可以是 "yyyy-mm-dd”。
// zipcode 需要對照到各縣市各區的郵遞區號，可以參考 郵遞區號速查一覽表。
// 串接 API 時需避免在伺服器端與客戶端重複發送請求。
// await $fetch(url, {
//   method: "",
//   body: {},
//   baseURL: "",
//   query: {},
//   params: {}
//   headers: {},
// })