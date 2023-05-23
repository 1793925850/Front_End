<template>
    <div class="aside">
        <h3>AsideVue</h3>
        <ItemVue/>
        <ItemVue/>
        <ItemVue/>
    </div>
</template>

<script>
import ItemVue from "@/pager/ItemVue.vue";
export default {
    components:{
        ItemVue,
    }
}
</script>

<style scoped>
.aside{
    float: right;
    width: 29%;
    height: 600px;
    border: 5px solid #999;
    box-sizing: border-box;
}
</style>