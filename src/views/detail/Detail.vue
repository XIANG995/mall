<template>
  <div id="detail">
    <detail-nav-bar></detail-nav-bar>
  </div>
</template>

<script>
  import DetailNavBar from './childComps/DetailNavBar'

  import {getDetailData} from 'network/detail'

 
  export default {
    name: 'Detail',
    data() {
      return {
        iid: null
      }
    },
    components: {
      DetailNavBar
    },
    created() {
      this.iid = this.$route.params.iid;
      getDetailData(this.iid).then(res => {
        console.log(res);
      })
    }
  };
</script>

<style scoped>

</style>
