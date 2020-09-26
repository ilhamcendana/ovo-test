<template>
  <CBox py="20px">
    <CButton
      bg="primary"
      color="#fff"
      v-if="!showAddInput"
      @click="showAddInput = !showAddInput"
      left-icon="add"
      width="100%"
      size="xs"
      :_hover="{ opacity: 0.8 }"
      :_active="{ opacity: 0.5 }"
      :_focus="{}"
    >
      Add More Currencies
    </CButton>

    <CFlex v-if="showAddInput">
      <c-select
        v-model="pickedCurrency"
        placeholder="Select Currencies"
        border="0"
        size="sm"
        @change="handleChangePickedCurrency"
      >
        <option v-for="name in listCurrencies" :key="name" :value="name">
          {{ name }}
        </option>
      </c-select>

      <CButton
        :isDisabled="pickedCurrency === ''"
        size="sm"
        bg="primary"
        color="#fff"
        border-radius="0 7px 7px 0"
        :_hover="{ opacity: 0.8 }"
        :_active="{ opacity: 0.5 }"
        :_focus="{}"
        @click="submitPickedCurrency"
        >Submit</CButton
      >
    </CFlex>
  </CBox>
</template>

<script>
import { CBox, CSelect, CButton, CFlex } from "@chakra-ui/vue";

export default {
  name: "BottomAction",
  components: {
    CBox,
    CButton,
    CSelect,
    CFlex,
  },
  data() {
    return {
      listCurrencies: [
        "USD",
        "CAD",
        "IDR",
        "GBP",
        "CHF",
        "SGD",
        "INR",
        "MYR",
        "JPY",
        "KRW",
      ],
      showAddInput: false,
      pickedCurrency: "",
    };
  },
  methods: {
    handleChangePickedCurrency: function (e) {
      this.pickedCurrency = e;
    },
    submitPickedCurrency: function () {
      this.$emit("sendPickedCurrency", this.pickedCurrency);
      this.pickedCurrency = "";
      this.showAddInput = false;
    },
  },
};
</script>

<style>
</style>