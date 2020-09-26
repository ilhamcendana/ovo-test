<template>
  <CFlex
    mb="20px"
    box-shadow="0px 0px 10px rgba(0,0,0,.1)"
    border-radius="10px"
    py="20px"
    justify-content="space-evenly"
    align-items="center"
  >
    <CBox border-right="1px solid #999" px="10px" w="85%">
      <CFlex
        w="100%"
        justify-content="space-between"
        font-size="xl"
        font-weight="bold"
      >
        <CText mr="5px">{{ name }}</CText>
        <CText overflow="hidden">{{
          (Math.round(value * initialValue * 100) / 100)
            .toFixed(2)
            .toString()
            .replace(/\B(?=(\d{3})+(?!\d))/g, ".")
        }}</CText>
      </CFlex>

      <CText font-size="sm">{{ name }} - {{ currenciesName[name] }}</CText>
      <CText font-size="sm"
        >1 USD =
        {{
          (Math.round(value * 100) / 100)
            .toFixed(2)
            .toString()
            .replace(/\B(?=(\d{3})+(?!\d))/g, ".")
        }}
        {{ name }}</CText
      >
    </CBox>

    <CButton
      px="10px"
      w="15%"
      variant="ghost"
      size="xs"
      :_hover="{ opacity: 0.8 }"
      :_active="{ opacity: 0.5 }"
      :_focus="{}"
      @click="$emit('delete-currency', name)"
    >
      <CIcon name="minus" color="#b93333" />
    </CButton>
  </CFlex>
</template>

<script>
import { CFlex, CBox, CText, CIcon, CButton } from "@chakra-ui/vue";

export default {
  name: "CurrencyItem",
  components: {
    CFlex,
    CBox,
    CText,
    CIcon,
    CButton,
  },
  props: ["name", "value", "initialValue"],
  data() {
    return {
      currenciesName: {
        USD: "Unites States Dollars",
        CAD: "Canadian Dollar",
        IDR: "Indonesian Rupiah",
        GBP: "Pound Sterling",
        CHF: "Swiss Franc",
        SGD: "Singapore Dollar",
        INR: "Indian Rupee",
        MYR: "Malaysian Ringgit",
        JPY: "Japanese Yen",
        KRW: "South Korean Won",
      },
    };
  },
};
</script>
