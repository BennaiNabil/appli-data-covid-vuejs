<template>
  <div id="app">
    <Header/>
    <div class="container">
      <Home/>
    </div>
  </div>
</template>

<script>
import Home from "./components/Home";
import Header from "./components/Header";

export default {
  name: 'App',
  components: {
    Home,
    Header
  }
}
</script>
