<template>
  <!-- <li v-for="device in devices" :key="device.id">
    {{ device.id }} - {{ device.DeviceName }}
  </li> -->
  <!-- v-for require key-->
  <!-- :key = v-bind (11:47)-->
  <!--bind ใช้เพื่อบอกว่าเราจะเอา ตัวแปรในscriptมาใช้ถ้าไม่ใส่มันจะมองว่าโค๊ดที่เราจะ get data เป็นแค่ string-->
  <h1 class="font-black mb-3">Devices</h1>
  <div class="grid grid-cols-3 gap-4 border border-black ml-0 mr-5 p-3">
    <ul v-for="device in devices" :key="device.id">
      <li>
        <router-link :to="{ name: 'device', params: { id: device.id } }">
          <img :src="device.Photo" />
        </router-link>
      </li>
    </ul>
  </div>
</template> //html

<script>
import axios from "axios";
export default {
  //ประกาศ prop
  props: {
    manufacturerId: Number,
  },
  //ประกาศ data
  data: () => ({
    devices: [
      { id: 1, DeviceName: "ASUS ROG" },
      { id: 2, DeviceName: "DELL PREDATOR" },
    ],
  }),
  //end of data
  created() {
    console.log("manufacturerId : ", this.manufacturerId);

    if (this.manufacturerId !== 0) {
      axios
        .get(
          `https://service2.ahead-coop.work/devices?ManufacturerID=${this.manufacturerId}`
        )
        .then((res) => {
          this.devices = res.data;
        });
    } else {
      axios.get(`https://service2.ahead-coop.work/devices`).then((res) => {
        this.devices = res.data;
      });
    }
  },
  //end of created
  watch: {
    manufacturerId: function (newID, oldID) {
      console.log(`new : ${newID}, old ${oldID}`);
      this.getDeviceByManufacturer(newID);
    },
  },
  //end of watch
  methods: {
    getDeviceByManufacturer(id) {
      axios
        .get(`https://service2.ahead-coop.work/devices?ManufacturerID=${id}`)
        .then((res) => {
          this.devices = res.data;
        });
    },
  },
  //end of methods GetDeviceByID
};
</script> //js