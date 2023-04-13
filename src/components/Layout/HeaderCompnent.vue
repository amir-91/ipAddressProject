<template>
  <header>
    <div class="container">
      <div class="row">
        <div class="col-12 header__title">
          <h1>IP Address Tracker</h1>
        </div>
        <div class="col-10 input-group mb-3">
          <input
            v-model="ipOrDomain"
            type="text"
            class="form-control"
            placeholder="Search for any IP Address or Domain"
            aria-label="Search for any IP Address or Domain"
            aria-describedby="button-addon2"
            @keyup.enter="searchByIpOrDomain(ipOrDomain)"
          />
          <button
            class="btn btn-outline-secondary"
            type="button"
            id="button-addon2"
            @click="searchByIpOrDomain(ipOrDomain)"
          >
            <ion-icon name="chevron-forward-outline"></ion-icon>
          </button>
        </div>
        <div class="header__error" v-if="!isValidIp && isValidOnMount">
          please enter valid ip address
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: ["isValidIp"],
  data() {
    return {
      ipOrDomain: this.currentIp,
      ipData: [],
      currentIp: "",
      isValidOnMount: false
    };
  },
  methods: {
    searchByIpOrDomain(currentIp) {
      this.$emit("ip", currentIp);
      this.isValidOnMount = true
    },
  },
};
</script>
