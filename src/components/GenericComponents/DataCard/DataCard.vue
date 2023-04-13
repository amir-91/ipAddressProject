<template>
  <div class="container data-card">
    <div v-if="!isLoading" class="row data-card__body">
      <div class="col-lg-3 col-md-3 col-12">
        <p class="data-card__body__title">IP ADDRESS</p>
        <p class="data-card__body__subtitle">{{ ipAddress }}</p>
      </div>
      <div class="col-lg-3 col-md-3 col-12">
        <p class="data-card__body__title">LOCATION</p>
        <p class="data-card__body__subtitle">{{ location }}</p>
      </div>
      <div class="col-lg-3 col-md-3 col-12">
        <p class="data-card__body__title">TIMEZONE</p>
        <p class="data-card__body__subtitle">{{ timeZone }}</p>
      </div>
      <div class="col-lg-3 col-md-3 col-12">
        <p class="data-card__body__title">ISP</p>
        <p class="data-card__body__subtitle">{{ isp }}</p>
      </div>
    </div>
    <div class="loader-container" v-else>
        <img src="../../../assets/images/loading-gif.gif" />
      </div>
  </div>
</template>

<script>
export default {
  props: ["ipAddress", "location", "timeZone", "isp","isLoading"],
};
</script>
