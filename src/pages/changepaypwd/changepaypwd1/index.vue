<template>
  <div class="changepaypwd1">
    <phone @getcode=getcode @nextbtn=nextbtn></phone>
  </div>
</template>

<script>
import phone from "../../../components/phoneProving.vue";
export default {
  name: "changepaypwd1",
  components: {
    phone
  },
  props: [],
  data() {
    return {};
  },
  created() {},
  mounted() {},
  methods: {
    getcode(str) {
      alert(str);
    },
    nextbtn(str) {
      alert(str);
      this.$router.push("/changepaypwd2");
    }
  }
};
</script>
<style scoped lang="scss">

</style>