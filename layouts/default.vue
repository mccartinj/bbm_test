<template>
  <div class="container">
    <nuxt />
  </div>
</template>

<style lang="scss">
html {
  font-family: Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

body {
  //overflow: hidden;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

a {
  text-decoration: underline;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  min-width: 100vw;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: Arial, sans-serif;
  display: block;
  font-weight: 700;
  font-size: 2.4em;
  color: #35495e;
  letter-spacing: 1px;
  position: relative;
  z-index: 1000;

  a:hover {
    text-decoration: underline;
  }
}

.links {
  padding-top: 15px;
}

.inner {
  height: 100vh;
  width: 100vw;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
