<template>
  <div>
    <div class="navbar">
      <img class="meni" src="@/assets/meni.png" />
      <a><img class="title" src="@/assets/title.png" /></a>
      <img class="map" src="@/assets/map.png" />
    </div>
    <div class="box-inf">
      <button @click="filteredlaptime()">jsijx</button>
      <div class="dropdown">
        <button class="dropbtn">Dropdown</button>
        <div class="dropdown-content">
          <a href="#">Link 1</a>
          <a href="#">Link 2</a>
          <a href="#">Link 3</a>
        </div>
      </div>
      <div v-for="item in data" :key="item.id">
        {{ item.id }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [],
      data2: [],
    };
  },

  async created() {
    // GET request using fetch with async/await
    const response = await fetch(
      "https://pacenotes.seleven.de/lap-service/rest/lap?limit=20"
    );
    const data = await response.json();
    this.data = data;
    console.log(data);
  },
  computed: {
    filteredlaptime() {
      let laptime = this.data;

      laptime = laptime.filter((item) => {
        return item.driverVehicle == "E92 M3";
      });
    },
  },
};
</script>



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
  width: auto;
  height: auto;
  background-color: $color;
  margin-top: 60spx;
  border-radius: 15px;
  margin: auto;
  text-align: center;
}
.title {
  width: 500px;
  height: 100%;
}
.b_sort {
  width: $width;
  height: 55px;
  float: right;
  cursor: pointer;
  margin-right: $margin-sides;
}
.dropbtn {
  width: $width;
  height: 55px;
  float: right;
  cursor: pointer;
  margin-right: $margin-sides;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content a:hover {
  background-color: #ddd;
}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown:hover .dropbtn {
  background-color: #3e8e41;
}
</style>
