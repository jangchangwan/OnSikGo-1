<template>
  <div>
    <div
      v-for="(users, index) in userList"
      :key="index"
      class="row text-start">
      <div class="content">
      <div class="detail text-start">
        <p class="text-primary">π μ¬μ©μλͺ: {{ users.userName }}</p>
        <p>λλ€μ: {{ users.nickname }}</p> 
      </div>
        <img
          class="siren"
          src="@/assets/images/trash.png"
          @click="deleteUser(users)"
          alt="μ­μ λ²νΌμ΄μλκ².."
        />
      </div>
      <hr class="mt-2">
    </div>
  </div>
</template>

<script>
import http from "@/util/http-common";

export default {
  name : 'AdminUser',

  data: function () {
    return {
      userList: [],
    }
  },

  methods: {
    allUser() {
      http
        .get('/user/total')
        .then((response) => {
          this.userList = response.data;
        })

    },
    
    deleteUser(users) {
      http
        .delete(`/admin/${users.email}`)
        .then((response) => {
          if (response.status == 200) {
            this.allUser();
          }
        });
    },
  },

  created () {
  this.allUser();
  }
};
</script>

<style>
.content{
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-left: 5%;
  margin-right: 5%;
}
.detail{
  width: 320px;
}
.siren {
  width: 25px;
  height: 25px;
}
</style>