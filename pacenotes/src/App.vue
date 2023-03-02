<template>
  <div>
    <div class="navbar">
      <div class="dropdown">
        <img class="meni" src="@/assets/meni.png" />
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

      <a><img class="title" src="@/assets/title.png" /></a>
      <img class="map" src="@/assets/map.png" />
    </div>
    <div class="box-inf">
      <div
        v-if="
          activeEndpoint ===
          'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=laptime'
        "
      >
        <h1>Sort by Laptime</h1>
        <form @submit.prevent="showInformationByMonthAndYear">
          <label for="month">Select a month:</label>
          <select v-model="selectedMonth" name="month" id="month">
            <option
              v-for="(month, index) in months"
              :key="index"
              :value="index + 1"
            >
              {{ month }}
            </option>
          </select>
          <label for="year">Select a year:</label>
          <input
            v-model.number="selectedYear"
            type="number"
            name="year"
            id="year"
            min="1900"
            max="2100"
          />
          <button type="submit" @click="showDiv = !showDiv">
            Show information
          </button>
        </form>

        <div v-if="information.length > 0">
          <div v-for="(item, index) in information" :key="index">
            Driver name: {{ item.driverName }} Laptime:
            {{ item.laptime }} Drivers Viacle: {{ item.driverVehicle }} Date:
            {{ item.date }}
          </div>
        </div>

        <div v-if="showDiv">
          <div v-for="item in data2" :key="item.id">
            Driver name: {{ item.driverName }} Laptime:
            {{ item.laptime }} Drivers Viacle: {{ item.driverVehicle }} Date:
            {{ item.date }}
          </div>
        </div>
      </div>
      <div
        v-if="
          activeEndpoint ===
          'https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=date'
        "
      >
        <h1>Sort by Date</h1>
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
        <h1>Sort by Driver Vehicle</h1>
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
        <h1>Sort by Driver Name</h1>
        <div v-for="item in data5" :key="item.id">
          Driver name: {{ item.driverName }} Laptime: {{ item.laptime }} Drivers
          Viacle: {{ item.driverVehicle }} Date: {{ item.date }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      data: [],
      data2: [],
      data3: [],
      data4: [],
      data5: [],
      information: [],

      showDiv: true,
      activeEndpoint: [],

      selectedMonth: new Date().getMonth() + 1,
      selectedYear: new Date().getFullYear(),
      months: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
      endpointUrl:
        "https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=laptime",
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
    async showInformationByMonthAndYear() {
      try {
        const response = await axios.get(
          `https://pacenotes.seleven.de/lap-service/rest/lap?limit=100&orderby=laptime`
        );

        const filteredInformation = response.data.filter((item) => {
          const date = new Date(item.date);
          const year = date.getFullYear();
          const month = date.getMonth() + 1;
          return year === this.selectedYear && month === this.selectedMonth;
        });

        this.information = filteredInformation;
      } catch (error) {
        console.log(error);
      }
    },

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

  computed: {
    /*
    sortedOptions() {
      return this.data.sort((a, b) => a.driverName.localeCompare(b.driverName));
    },
    */
    // Calculate the items to display on the current page
    itemsToShow() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.data.slice(startIndex, endIndex);
    },
    slicedData() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.data.slice(start, end);
    },
  },
};
</script>



<style lang="scss">
$width: 150px;
$margin-top: 10px;
$margin-sides: 20px;
$color: #333;

body {
  background-color: #717070;
  margin: 0;
  font-family: Arial, sans-serif;
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
  width: 60px;
  height: 60px;
  float: left;
  margin-top: $margin-top;
  margin-left: $margin-sides;
  cursor: pointer;
}

.map {
  width: 60px;
  height: 60px;
  float: right;
  cursor: pointer;
  margin-top: $margin-top;
  margin-right: $margin-sides;
}

.box-inf {
  width: 850px;
  height: auto;
  background-color: $color;
  margin: auto;
  margin-top: 60px;
  border-radius: 15px;
  text-align: center;
  line-height: 50px;
  color: #f1f1f1;
}

.title {
  width: 500px;
  height: 100%;
}

.dropbtn {
  position: absolute;
  top: 0;
  right: 0;
  padding: 10px;
  background-color: blue;
  color: white;
  border: none;
  position: relative;
  float: right;
  margin-top: 10px;
  margin-right: 10px;
}

.dropdown {
  position: relative;
  float: left;
  margin-right: 10px;
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
