<template>
  <nav role="navigation" class="header">
    <a href="https://www.restplatzboerse.at/" target="_blank" role="link"
      ><img src="../assets/logo.svg" alt="Restplatzbörse" class="logo"
    /></a>
  </nav>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100vw;
  height: 80px;

  margin: 0 auto;
  box-shadow: 0 2px 6px 2px #ccc;
}

.logo {
  height: 48px;
  min-height: 24px;
  max-height: calc(100vw / 12);
  margin-left: 15px;
}
</style>
