<template>
  <div v-if="!isError" class="container-fluid IpSearch">
    <Header :isValidIp="isValidIp" @ip="getIpData($event)"></Header>
    <div v-if="!isError" class="row">
      <div v-if="!isLoading" class="col-12 IpSearch__map-container">
        <DataCard
          :ipAddress="ipData.ip"
          :location="ipData.location.city"
          :timeZone="ipData.location.timezone"
          :isp="ipData.isp"
          :isLoading="isDtaCardLoading"
        ></DataCard>
        <MapComponent :center="ipData.location"></MapComponent>
      </div>
      <div class="loader-container" v-else>
        <img src="../../assets/images/loading-gif.gif" />
      </div>
    </div>
  </div>
  <ErrorPage v-else></ErrorPage>
</template>

<script>
import DataCard from "../../components/GenericComponents/DataCard/DataCard.vue";
import Header from "../../components/Layout/HeaderCompnent.vue";
import MapComponent from "../../components/MapComponent/MapComponent.vue";
import ErrorPage from "@/components/GenericComponents/ErrorPage/ErrorPage.vue";
import {
  getIpAddressData,
  getCurrentIpAddress,
} from "../../services/services.js";
export default {
  components: { DataCard, Header, MapComponent, ErrorPage },
  data() {
    return {
      ipData: {
        ip: "",
        location: "",
        timezone: "",
        isp: "",
      },
      currentIp: "",
      isValidIp: true,
      isLoading: true,
      isDtaCardLoading: false,
      isError: false,
    };
  },
  methods: {
    callIpAddressApi() {
      getIpAddressData(
        `https://geo.ipify.org/api/v2/country,city?apiKey=at_zgeR35LvamY6wa5Dt9IhVzlREy1Fs&ipAddress=${this.currentIp}`,
        (res) => {
          if (res.status == 200) {
            this.isLoading = false;
            this.isError = false;
            this.isDtaCardLoading = false;
            this.ipData = {
              ip: res.data.ip,
              location: res.data.location,
              timezone: res.data.location.timezone,
              isp: res.data.isp,
            };
          } else {
            this.isLoading = false;
          }
        },
        () => {
          this.isLoading = false;
          this.isError = true;
        }
      );
    },
    getIpData(ip) {
      this.isDtaCardLoading = true;
      this.currentIp = ip;
      let ipRegex =
        /^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/;
      if (this.currentIp && this.currentIp.match(ipRegex)) {
        this.isValidIp = true;
        this.callIpAddressApi();
      } else {
        this.isValidIp = false;
        this.isDtaCardLoading = false;
      }
    },
  },
  mounted() {
    getCurrentIpAddress(
      "https://api64.ipify.org/?format=json",
      (res) => {
        this.currentIp = res.data.ip;
      },
      (err) => {
        console.log(err);
      }
    );
    this.getIpData(this.currentIp);
    this.callIpAddressApi();
  },
};
</script>
