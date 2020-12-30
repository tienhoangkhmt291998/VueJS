<template>
    <div class="block">
      <el-pagination
      layout="prev, pager, next, slot" 
      :total="this.$store.state.NumberPages"
     @current-change="handlePagination" 
     > </el-pagination>
    </div>
</template>

<script>
export default {
    data () {
        return {
            insidePage:1
        }
    },
   methods: {
      handlePagination (index) {
          let indexPages = index -1;
          let Index = indexPages* 10;
          let currentIndex = Index + 10;
          this.$store.state.index = Index;
          this.$store.state.currentIndex = currentIndex
      },
   }
};
</script>

<style>
</style>