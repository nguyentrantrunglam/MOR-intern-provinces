<template>
  <div class="selectProvince">
    <input
      v-model="inpValue"
      class="search"
      type="text"
      placeholder="Chọn tỉnh thành"
      v-on:click="deleteInput"
    />
    <font-awesome-icon class="dropdown-btn" icon="fa-solid fa-caret-down" />
  </div>
</template>

<script>
export default {
  name: "SelectProvince",
  props: ["inputValue"],
  data() {
    return {
      inpValue: "",
      displayList: "block",
    };
  },
  methods: {
    deleteInput() {
      this.inpValue = "";
    },
  },
  watch: {
    inpValue() {
      this.$emit("updateListProvince", this.displayList);
      this.$emit("updateInputValue", this.inpValue);
    },
    inputValue: {
      handle() {
        this.inpValue = this.inputValue;
      },
      deep: true,
    },
  },
};
</script>

<style scoped>
*:focus {
  outline: none;
}

.selectProvince {
  box-sizing: border-box;
  position: absolute;
  width: 480px;
  height: 48px;
  left: 80px;
  top: 104px;
  background: #ffffff;
  border: 1px solid #007bc3;
  box-shadow: 0px 0px 8px rgba(0, 123, 195, 0.32);
  border-radius: 4px;
}
.selectProvince_text {
  position: absolute;
  left: 16px;
  top: 16.13%;
  bottom: 81.72%;
  font-family: Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  display: flex;
  align-items: center;
  color: #999999;
}
input[type="text"] {
  outline: none;
}

.search {
  width: 80%;
  margin-left: 16px;
  margin-top: 13px;
  font-size: 16px;
  border: none;
}
.dropdown-btn {
  position: absolute;
  right: 16px;
  top: 14px;
  width: 8px;
  cursor: pointer;
}
</style>