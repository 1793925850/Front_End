<template>
  <HeaderVue />
  <MainVue />
  <AsideVue />
</template>

<script>
import HeaderVue from "@/pager/HeaderVue.vue";
import MainVue from "@/pager/MainVue.vue";
import AsideVue from "@/pager/AsideVue.vue";
export default {
    components:{
        HeaderVue,
        MainVue,
        AsideVue,
    }
}
</script>