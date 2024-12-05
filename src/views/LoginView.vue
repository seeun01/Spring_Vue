<template>
  <div class="flex items-center justify-center h-screen bg-slate-50">
    <div class="w-4/12 m-10 p-10 border-solid border-2  rounded-xl shadow-md bg-white">
      <div class="flex items-center justify-center p-4 gap-3">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-9">
          <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75 11.25 15 15 9.75m-3-7.036A11.959 11.959 0 0 1 3.598 6 11.99 11.99 0 0 0 3 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285Z" />
        </svg>
        <h1 class="font-black text-3xl">cube login</h1>
      </div>
      <div class="p-4">
        <h2 class="font-extrabold text-lg">PW 인증</h2>
      </div>
      <div class="p-4">
        <div class="relative">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="absolute left-7 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-500 size-6">
            <path fill-rule="evenodd" d="M18.685 19.097A9.723 9.723 0 0 0 21.75 12c0-5.385-4.365-9.75-9.75-9.75S2.25 6.615 2.25 12a9.723 9.723 0 0 0 3.065 7.097A9.716 9.716 0 0 0 12 21.75a9.716 9.716 0 0 0 6.685-2.653Zm-12.54-1.285A7.486 7.486 0 0 1 12 15a7.486 7.486 0 0 1 5.855 2.812A8.224 8.224 0 0 1 12 20.25a8.224 8.224 0 0 1-5.855-2.438ZM15.75 9a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z" clip-rule="evenodd" />
          </svg>
          <input v-model="userId" type="text" placeholder="dwhan" class="bg-gray-100 rounded-full pl-14 p-3 m-1 w-full"/>
        </div>
        <div class="relative">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="absolute left-7 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-500 size-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 1 0-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 0 0 2.25-2.25v-6.75a2.25 2.25 0 0 0-2.25-2.25H6.75a2.25 2.25 0 0 0-2.25 2.25v6.75a2.25 2.25 0 0 0 2.25 2.25Z" />
          </svg>
          <input v-model="userPw" type="password" placeholder="비밀번호를 입력해주세요." class="border-solid border-2 rounded-full pl-14 p-3 m-1 w-full"/>
        </div>
        <div>
          <button @click="loginSubmit" class="bg-slate-700 rounded-full text-center text-white w-full m-1 h-10">로그인</button>
        </div>
      </div>
      <div class="mt-32 p-4">
        <div class="flex items-center justify-center gap-3">
          <div class="border-t border-gray-500 w-1/4"></div>
          <h3 class="font-bold">다른 인증수단 선택</h3>
          <div class="border-t border-gray-500 w-1/4"></div>
        </div>
        <div class="flex items-center justify-center m-5">
          <div class="w-20 h-20 border-gray-800 border rounded-3xl shadow-md flex items-center justify-center">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-12">
              <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 1 0-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 0 0 2.25-2.25v-6.75a2.25 2.25 0 0 0-2.25-2.25H6.75a2.25 2.25 0 0 0-2.25 2.25v6.75a2.25 2.25 0 0 0 2.25 2.25Z" />
            </svg>
          </div>
        </div>
        <p class="text-xs">PW</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      userId : null,
      userPw : null,
    }
  },
  methods: {
    loginSubmit() {
      let saveData = {};
      saveData.userId = this.userId;
      saveData.userPw = this.userPw;

      console.log(saveData);

      axios.post("http://10.10.30.105:8080/signin", saveData, {
        headers: {
          "Content-Type": "application/json"
        }
      })
          .then((response) => {
            console.log(response);
            alert("로그인 성공");
            this.$router.push("/");
          })
          .catch((error) => {
            console.log(error);
            this.userId = null;
            this.userPw = null;
            alert("로그인 실패")
          })
      }
  }
}
</script>