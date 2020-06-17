<template>
  <div id="app">
    <header>ヘッダー</header>
    <div class="container">
      <main>収支</main>
      <div class="column">
        <aside>収入</aside>
        <aside>支出</aside>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
#app {
  width: 1000px;
  margin: 0 auto;
}
.container {
  display: flex;
}
.column {
  flex-direction: column;
}
main {
  flex: 1;
  height: 1000px;
}
aside {
  width: 450px;
  height: 500px;
}
</style>