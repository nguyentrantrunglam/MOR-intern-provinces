<template>
  <div class="listProvince">
    <ul class="listProvince-items">
      <li
        v-for="province in filteredItems"
        :key="province.code"
        class="listProvince-item container"
      >
        <label :for="province.code"
          >{{ province.name }}
          <input
            class="checkbox"
            :id="province.code"
            :value="province.name"
            type="checkbox"
            v-model="selected"
            @input="checkEmpty" />
          <span class="checkmark"></span
        ></label>
      </li>
    </ul>
    <div class="listProvince-buttons">
      <button
        :disable="isDisableButton"
        @click="sendData"
        class="button-confirm"
        :disabled="!selected"
      >
        Đồng ý
      </button>
      <button @click="cancel" class="button-cancel">Hủy</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListProvince",
  props: ["inputValue", "selectedProvinces"],
  data() {
    return {
      provinces: [],
      selected: [],
      enable: false,
      bgColor: "#DCDCDC",
      displayShow: true,
      displayList: "none",
      inputValueEmpty: "",
      isDisableButton: true,
      cursor: "context-menu",
    };
  },

  async mounted() {
    const res = await fetch("https://provinces.open-api.vn/api/?depth=3");
    this.provinces = await res.json();
    return this.provinces;
  },
  methods: {
    sendData() {
      this.$emit("updateProvince", this.selected);
      this.$emit("updateEnable", this.enable);
      this.$emit("updateInputValueEmpty", this.inputValueEmpty);
      if (this.selected.length != 0) {
        this.$emit("updateShowProvince", this.displayShow);
        this.$emit("updateListProvince", this.displayList);
      } else {
        this.$emit("updateShowProvince", !this.displayShow);
      }
    },
    cancel() {
      this.$emit("updateListProvince", this.displayList);
      this.$emit("updateProvince", []);
    },
  },

  computed: {
    btnStyle() {
      return {
        "background-color": this.bgColor,
      };
    },
    filteredItems() {
      return this.provinces.filter((province) => {
        return province.name
          .toLowerCase()
          .normalize("NFD")
          .replace(/[\u0300-\u036f]/g, "")
          .includes(
            this.inputValue
              .toLowerCase()
              .normalize("NFD")
              .replace(/[\u0300-\u036f]/g, "")
          );
      });
    },
  },
  watch: {
    selected: {
      handler() {
        if (this.selected.length == 0) {
          this.bgColor = "#DCDCDC";
          this.isDisableButton = true;
          this.cursor = "context-menu";
        } else {
          this.bgColor = "#007BC3";
          this.isDisableButton = false;
          this.cursor = "pointer";
        }
      },
      deep: true,
    },
  },
};
</script>

<style scoped>
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 4px;
  left: 0;
  height: 16px;
  width: 16px;
  background-color: #fff;
  border-radius: 2px;
  border: 1px solid #000
}

.checkmark:active{
  border: none;
}

/* On mouse-over, add a grey background color */

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #45D1C9;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 6px;
  top: 2px;
  width: 4px;
  height: 8px;
  border: solid white;
  border-width: 0 1px 1px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
  
}

.listProvince {
  min-height: 36px;
  width: 480px;
  max-height: 304px;
  height: fit-content;
  position: absolute;
  left: 80px;
  top: 152px;
  background: #ffffff;
  box-shadow: 0px 1px 8px rgba(102, 102, 102, 0.2);
  border-radius: 4px;
}

.listProvince-items {
  min-height: 36px;
  max-height: 240px;
  height: fit-content;
  overflow-y: scroll;
}

.listProvince-item {
  height: 24px;
  margin-bottom: 16px;
  font-family: Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  display: flex;
  justify-content: left;
  color: black;
}
label {
  cursor: pointer;
}
p {
  margin: 0;
  margin-left: 10px;
}

.checkbox {
  width: 16px;
  height: 16px;
  margin-top: 4px;
  margin-right: 10px;
  cursor: pointer;
}

ul {
  margin: 0;
  list-style-type: none;
  padding-top: 20px;
  padding-left: 20px;
}

.listProvince-buttons {
  padding-left: 16px;
}

.button-confirm {
  margin-bottom: 16px;
  height: 32px;
  width: 104px;
  background: v-bind(bgColor);
  border-radius: 4px;
  font-family: Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  border: none;
  color: #ffffff;
  cursor: v-bind(cursor);
}

.button-cancel {
  height: 24px;
  width: 82px;
  background: white;
  border-radius: 4px;
  font-family: Arial, Helvetica, sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  border: none;
  color: #007bc3;
  cursor: pointer;
}
input[type="checkbox"] {
  accent-color: #45d1c9;
}

/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #fff;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #dcdcdc;
  border-radius: 6px;
  width: 8px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>  