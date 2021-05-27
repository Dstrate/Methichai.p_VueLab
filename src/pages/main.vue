<template>
  <div class="container">
    <manufacturer v-slot="data">
      <devices :manufacturerId="data.factID"></devices>
    </manufacturer>
  </div>
</template>

<script>
import Manufacturer from "@/components/Manufacturer.vue";
import Devices from "@/components/Device.vue";
export default {
  components: {
    Manufacturer: Manufacturer,
    Devices: Devices,
  },
};
</script>