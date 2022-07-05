<template>
  <div class="showProvince" style="style">
    <div
      v-for="(province, index) in selectedProvinces"
      :key="index"
      :id="index"
      class="province-tag"
    >
      <p class="province-name">{{ province }}</p>
      <font-awesome-icon
        v-on:click="removeElement(index)"
        class="x-btn"
        icon="fa-solid fa-x"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "ShowProvince",
  props: ["selectedProvinces"],
  data() {
    return {
      selected:this.selectedProvinces,
    };
  },

  methods: {
    removeElement(index) {
      this.selected.splice(index, 1);
    },
  },
  watch: {
    selectedProvinces(){
      this.selected = this.selectedProvinces
    },
    selected() {
      this.$emit("updateProvince", this.selected);
    },
  },
};
</script>

<style scoped>
.showProvince {
  box-sizing: border-box;
  position: absolute;
  width: 480px;
  min-height: 48px;
  height: fit-content;
  left: 80px;
  top: 156px;
  background: #ffffff;
  border: 1px solid #007bc3;
  border-radius: 4px;
  z-index: -1;
  display: flex;
  justify-content: flex-start;
  background: #ffffff;
  border: 1px solid #999999;
  border-radius: 4px;
  flex-wrap: wrap;
  padding-bottom: 8px;
}

.province-tag {
  min-width: 90px;
  height: 32px;
  background: #f8f8f8;
  border-radius: 32px;
  color: #333333;
  margin-top: 8px;
  display: flex;
  padding-left: 16px;
  padding-right: 16px;
  justify-content: space-around;
}
.province-name {
  margin-top: 8px;
  font-family: Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  margin-right: 12px;
}

.x-btn {
  margin-top: 10px;
  width: 11px;
  height: 11px;
}
</style>