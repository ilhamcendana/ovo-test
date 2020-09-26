<template>
  <div class="container">
    <CBox v-bind="mainStyles[colorMode]" min-height="100vh">
      <Header
        :initialValue="initialValue.toString()"
        v-on:changeValue="changeValue"
      />

      <CBox w="100%" d="flex" justify-content="center">
        <CBox px="20px" :w="['100%', '500px', '700px', '75%']">
          <CurrencyList
            :rates="convertBox"
            :initialValue="initialValue"
            v-on:delete-currency="deleteCurrency"
          />
          <BottomAction
            :listCurrencies="data.rates"
            v-on:sendPickedCurrency="sendPickedCurrency"
          />
        </CBox>
      </CBox>
    </CBox>
  </div>
</template>

<script>
import { CBox } from "@chakra-ui/vue";
import Header from "../components/Header";
import CurrencyList from "../components/CurrencyList";
import BottomAction from "../components/BottomAction";
import axios from "axios";

export default {
  name: "App",
  inject: ["$chakraColorMode", "$toggleColorMode"],
  components: {
    CBox,
    Header,
    CurrencyList,
  },
  data() {
    return {
      mainStyles: {
        dark: {
          bg: "gray.700",
          color: "whiteAlpha.900",
        },
        light: {
          bg: "white",
          color: "gray.900",
        },
      },
      initialValue: 10.0,
      convertBox: {},
    };
  },
  computed: {
    colorMode() {
      return this.$chakraColorMode();
    },
    theme() {
      return this.$chakraTheme();
    },
    toggleColorMode() {
      return this.$toggleColorMode;
    },
  },
  methods: {
    changeValue: function (e) {
      this.initialValue = e;
    },
    sendPickedCurrency: function (currency) {
      let sample = { ...this.convertBox };
      sample[currency] = this.data.rates[currency];
      this.convertBox = sample;
    },
    deleteCurrency: function (name) {
      this.$delete(this.convertBox, name);
    },
  },
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://api.exchangeratesapi.io/latest?base=USD`
    );
    return { data: data };
  },
};
</script>
