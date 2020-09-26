<template>
  <CBox pt="20px">
    <CBox v-for="(value, name) in rates" :key="name">
      <CurrencyItem
        :name="name"
        :value="value"
        :initialValue="initialValue"
        v-on:delete-currency="$emit('delete-currency', name)"
      />
    </CBox>
  </CBox>
</template>

<script>
import { CBox } from "@chakra-ui/vue";
import CurrencyItem from "./CurrencyItem";

export default {
  name: "CurrencyList",
  components: {
    CBox,
    CurrencyItem,
  },
  props: ["rates", "initialValue"],
};
</script>
