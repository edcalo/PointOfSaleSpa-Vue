<template>
  <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
    <el-menu-item index="1">
      <router-link tag="a" :to="{path:'/home'}">Inicio</router-link>
    </el-menu-item>
    <el-menu-item class="ml-5" index="2">
      <router-link tag="a" :to="{path:'/clients'}">Clientes</router-link>
    </el-menu-item>
    <el-menu-item  v-if="role == 1" index="3">
      <router-link tag="a"  index="2-1" :to="{path:'/employes'}">Empleados</router-link>
    </el-menu-item>
    <el-menu-item index="5">
      <router-link tag="a" :to="{path:'/suppliers'}">Supplidores</router-link>
    </el-menu-item>
    <el-menu-item index="6">
      <router-link tag="a" :to="{path: '/products'}">Productos</router-link>
    </el-menu-item>

    <el-submenu class="acctions alert-to" index="7">
      <template slot="title">Acciones</template>
      <el-menu-item v-if="role != 1" index="2-1">
        <router-link tag="p" :to="{path:'/user/'+id}">Usuario</router-link>
      </el-menu-item>
      <el-menu-item index="2-2">
        <router-link tag="p" :to="{path:'/sale'}">Ventas</router-link>
      </el-menu-item>
      <el-menu-item index="2-3">
        <p @click="exit()">Salir</p>
      </el-menu-item>
    </el-submenu>
    <el-menu-item index="8">
      <span>{{userName}}</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
import { mapState, mapMutations } from "vuex";
export default {
  components: {
    alert
  },
  name: "Navbar",
  data: () => ({
    activeIndex: "1",
    activeIndex2: "1"
  }),
  methods: {
    ...mapMutations(["closeLogin"]),
    exit() {
      localStorage.clear();
      this.closeLogin();
      this.$router.push("/login");
    }
  },
  computed: {
    userName() {
      return JSON.parse(localStorage.getItem("user")).user;
    },
    role(){
      let user = JSON.parse(localStorage.getItem("user"));
      return user.userData.role
    },
    id(){
      let user = JSON.parse(localStorage.getItem("user"));
      return user.id
    }
  }
};
</script>

<style Scoped>
.alert-to {
  margin-left:40%;
}
</style>
