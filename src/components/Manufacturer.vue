<template>
  <!-- <li v-for="manufacture in manufacturer" :key="manufacture.id">
    {{ manufacture.id }} - {{ manufacture.Title }}
  </li> -->
  <!-- v-for require key-->
  <!-- :key = v-bind (11:47)-->
  <div class="grid grid-cols-2 gap-4 border-black">
    <div class="ml-10 mr-0">
      <h1 class="font-black mb-3">Manufacturer</h1>
      <ul
        class="border border-black"
        v-for="manufacture in manufacturer"
        :key="manufacture.id"
      >
        <li>
          <button @click="changeManufacturerId(manufacture.id)">
            <img :src="manufacture.Logo" width="100" />
          </button>
        </li>
      </ul>
    </div>
    <div>
      <slot :factID="currentManufactId"></slot>
    </div>
  </div>
</template> //html

<script>
import axios from "axios";
export default {
  //ประกาศ data
  data: () => ({
    //mock up data(test)
    currentManufactId: 0,
    manufacturer: [
      { id: 1, Title: "ASUS" },
      { id: 2, Title: "DELL" },
    ],
  }),
  //end of data
  created() {
    //assign data from server to manufacturer
    axios.get(`https://service2.ahead-coop.work/manufacturers`).then((res) => {
      // console.log(res.data);
      // response data from server
      this.manufacturer = res.data;
    });
  },
  //end of created
  methods: {
    changeManufacturerId(id) {
      this.currentManufactId = id;
      console.log("current id : ", this.currentManufactId);
    },
  },
  //end of methods ChangeManufactID
};
</script> //js