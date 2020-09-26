<template>
  <CBox
    w="100%"
    bg="primary"
    color="#fff"
    :px="['20px', '50px', '50px', '200px']"
    py="20px"
  >
    <CText fontSize="sm" mb="10px">USD - United Stated Dollars</CText>

    <CFlex
      w="100%"
      justifyContent="space-between"
      fontSize="xl"
      fontWeight="bold"
    >
      <CText w="25%">USD</CText>

      <CInput
        text-align="right"
        :_focus="{}"
        type="number"
        :value="initialValue"
        @change="changeHandler"
        background="none"
        border="none"
        fontSize="xl"
        fontWeight="bold"
      />
    </CFlex>
  </CBox>
</template>

<script>
import { CBox, CText, CFlex, CInput } from "@chakra-ui/vue";
export default {
  name: "Header",
  components: {
    CBox,
    CInput,
    CText,
    CFlex,
  },
  props: ["initialValue"],
  methods: {
    changeHandler: function (e) {
      this.$emit("changeValue", parseInt(e.target.value));
    },
  },
};
</script>
