<template>
  <div>
    <div class="navbar">
      <img class="meni" src="@/assets/meni.png" />
      <a><img class="title" src="@/assets/title.png" /></a>
      <img class="map" src="@/assets/map.png" />
    </div>
    <div class="box-inf"></div>
  </div>
</template>



<style lang="scss">
$width: 50px;
$margin-top: 17px;
$margin-sides: 10 px;
$color: #373030;
body {
  background-color: #717070;
  margin: 0;
}

.navbar {
  background-image: url("@/assets/navbar.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  height: 150px;
  text-align: center;
}
.meni {
  width: $width;
  height: 50px;
  float: left;
  margin-top: $margin-top;
  margin-left: $margin-sides;
  cursor: pointer;
}
.map {
  width: $width;
  height: 55px;
  float: right;
  cursor: pointer;
  margin-top: $margin-top;
  margin-right: $margin-sides;
}
.box-inf {
  width: 100px;
  height: auto;
  background-color: $color;
  margin-top: 60px;
  border-radius: 15px;
  margin: auto;
}
.title {
  width: 500px;
  height: 100%;
}
</style>
