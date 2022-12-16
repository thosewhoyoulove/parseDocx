<template>
    <div>
        这是parse
    </div>
</template>

<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router'
import { onMounted, reactive } from "vue";
const route = useRoute()
let data = route.query.data
onMounted(() => {
    console.log(data,'传过来的数据')
})
</script>

<style scoped>

</style>