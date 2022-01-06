<template>
  <Nav />
  <Header />
  <Home />
  <!-- <Reconversion /> -->
</template>

<script>
import Nav from './components/Nav.vue';
import Header from './components/Header.vue';
// import Reconversion from './views/Reconversion.vue';
import Home from './views/Home.vue';
export default {
  name: 'App',
  components: {
    // Reconversion,
    Nav,
    Header,
    Home,
  }
}
</script>