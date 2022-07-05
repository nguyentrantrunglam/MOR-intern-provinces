<template>
  <SelectProvince
    @updateListProvince="updateListProvince"
    @updateInputValue="updateInputValue"
    @click="handleEnableList"
    :inputValue="inputValue"
  />
  <ListProvince
    class="listProvince"
    :selectedProvinces="selectedProvinces"
    :inputValue="inputValue"
    @updateEnable="updateEnable"
    @updateProvince="updateProvince"
    @updateShowProvince="updateShowProvince"
    @updateListProvince="updateListProvince"
    @updateInputValueEmpty="updateInputValueEmpty"
  />
  <ShowProvince
    v-if="selectedProvinces.length"
    class="showProvince"
    :selectedProvinces="selectedProvinces"
    @updateProvince="updateProvince"
  />
  <span>{{inputValue}}</span>
</template>

<script>
import SelectProvince from "./components/SelectProvince.vue";
import ListProvince from "./components/ListProvince.vue";
import ShowProvince from "./components/ShowProvince.vue";
export default {
  name: "App",
  components: {
    SelectProvince,
    ListProvince,
    ShowProvince,
  },
  data() {
    return {
      displayList: "none",
      displayShow: false,
      selectedProvinces: [],
      inputValue: ''
    };
  },
  methods: {
    updateInputValue(inputValue) {
      this.inputValue = inputValue;
    },
    updateInputValueEmpty(inputValueEmty) {
      this.inputValue = inputValueEmty;
    },

    updateProvince(selected) {
      this.selectedProvinces = selected;
    },
    updateEnable(enable) {
      this.enable = enable;
    },
    updateShowProvince(displayShow) {
      this.displayShow = displayShow;
    },
    updateListProvince(displayList) {
      this.displayList = displayList;
    },
    handleEnableList() {
      if (this.displayList === "none") {
        this.displayList = "block";
      }
      else {
        this.displayList = "none";
      }
    },
  },
  computed: {
    listStyle() {
      return {
        display: this.displayList,
      };
    },
  },
};
</script>

<style>
.listProvince {
  display: v-bind(displayList);
}
</style>
