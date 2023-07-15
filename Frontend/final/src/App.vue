<template>
  <div class="container" style="background-color: khaki;">
    <nav class="nav-extended" :style="{ backgroundColor: menuColor }">
      <div class="nav-wrapper">
        <a href="#" class="brand-logo">UMSA Alumnos</a>
        <a href="#" data-target="mobile-demo" class="sidenav-trigger"><i class="material-icons">menu</i></a>
        <ul id="nav-mobile" class="right hide-on-med-and-down">
          <Menu></Menu>
        </ul>
      </div>
    </nav>

    <ul class="sidenav" id="mobile-demo" :style="{ backgroundColor: menuColor }">
      <Menu></Menu>
    </ul>
    <router-view />
  </div>
</template>

<style lang="scss"></style>

<script>
import Menu from '@/components/Menu.vue'
export default {
  name: 'AppView',
  components: {
    Menu
  },
  data() {
    return {
      menuColor: "darkslateblue"
    }
  },
  created() {
    document.addEventListener('DOMContentLoaded', function () {
      var elems = document.querySelectorAll('.sidenav');
      var instances = M.Sidenav.init(elems, {});
    });
  }
}
</script>
