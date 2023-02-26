<template>
  <div>
    <div class="navbar">
      <img class="meni" src="@/assets/meni.png" />
      <a><img class="title" src="@/assets/title.png" /></a>
      <img class="map" src="@/assets/map.png" />
    </div>
    <div class="box-inf">
      <div class="dropdown">
        <button class="dropbtn">Dropdown</button>
        <div class="dropdown-content">
          <a
            @click="
              setActiveEndpoint(
                'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=laptime'
              )
            "
            href="#"
            >Laptime</a
          >
          <a
            @click="
              setActiveEndpoint(
                'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=date'
              )
            "
            href="#"
            >Date</a
          >
          <a
            @click="
              setActiveEndpoint(
                'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=driver_vehicle'
              )
            "
            href="#"
            >Driver vehicle</a
          >
          <a
            @click="
              setActiveEndpoint(
                'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=driver_name'
              )
            "
            href="#"
            >Driver name</a
          >
        </div>
      </div>
      <div v-for="item in data" :key="item.id"></div>

      <div
        v-if="
          activeEndpoint ===
          'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=laptime'
        "
      >
        <div v-for="item in data2" :key="item.id">
          Driver name: {{ item.driverName }} Laptime: {{ item.laptime }} Drivers
          Viacle: {{ item.driverVehicle }} Date: {{ item.date }}
        </div>
      </div>
      <div
        v-if="
          activeEndpoint ===
          'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=date'
        "
      >
        <div v-for="item in data3" :key="item.id">
          Driver name: {{ item.driverName }} Laptime: {{ item.laptime }} Drivers
          Viacle: {{ item.driverVehicle }} Date: {{ item.date }}
        </div>
      </div>

      <div
        v-if="
          activeEndpoint ===
          'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=driver_vehicle'
        "
      >
        <div v-for="item in data4" :key="item.id">
          Driver name: {{ item.driverName }} Laptime: {{ item.laptime }} Drivers
          Viacle: {{ item.driverVehicle }} Date: {{ item.date }}
        </div>
      </div>

      <div
        v-if="
          activeEndpoint ===
          'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=driver_name'
        "
      >
        <div v-for="item in data5" :key="item.id">
          Driver name: {{ item.driverName }} Laptime: {{ item.laptime }} Drivers
          Viacle: {{ item.driverVehicle }} Date: {{ item.date }}
        </div>
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
      data3: [],
      data4: [],
      data5: [],
      activeEndpoint:
        "https://pacenotes.seleven.de/lap-service/rest/lap?limit=20",
    };
  },
  /*
  async created() {
    // GET request using fetch with async/await
    const response = await fetch(
      "https://pacenotes.seleven.de/lap-service/rest/lap?limit=20"
    );
    const data = await response.json();
    this.data = data;
    console.log(data);
  },
*/
  created() {
    this.getData();
    this.getDatadn();
    this.getDatadt();
    this.getDatadv();
    this.getDatalpt();
  },
  methods: {
    getData() {
      fetch("https://pacenotes.seleven.de/lap-service/rest/lap?limit=20")
        .then((response) => response.json())
        .then((data) => {
          this.data = data;
          console.log(data);
        });
    },
    getDatalpt() {
      fetch(
        "https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=laptime"
      )
        .then((response) => response.json())
        .then((data) => {
          this.data2 = data;
          console.log(data);
        });
    },

    getDatadt() {
      fetch(
        "https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=date"
      )
        .then((response) => response.json())
        .then((data) => {
          this.data3 = data;
          console.log(data);
        });
    },
    getDatadv() {
      fetch(
        "https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=driver_vehicle"
      )
        .then((response) => response.json())
        .then((data) => {
          this.data4 = data;
          console.log(data);
        });
    },
    getDatadn() {
      fetch(
        "https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=driver_name"
      )
        .then((response) => response.json())
        .then((data) => {
          this.data5 = data;
          console.log(data);
        });
    },
    setActiveEndpoint(endpoint) {
      this.activeEndpoint = endpoint;
    },
  },
  /*
  computed: {
    sortedOptions() {
      return this.data.sort((a, b) => a.driverName.localeCompare(b.driverName));
    },
  },*/
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
