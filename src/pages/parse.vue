<template>
    <div class="w-100vw h-100vh pt-5">

        <div
            class="flex w-20 h-20 bg-hex-5F9CEF border rounded-xl my-0 mx-auto text-hex-fff items-center justify-center">
            day
        </div>
        <div class="flex dashed-line text-center"></div>
        <div class=" border border-hex-5F9CEF mx-4 my-1">
            <div class="flex w-100% bg-hex-5F9CEF h-10 text-center items-center justify-center text-hex-fff">todo</div>
            <div class="text-xs p-3">
                <div class="flex">time</div>
                <div class="flex">place</div>
            </div>

            <div class="flex rectangle">
                <div class="absolute w-0 h-0 triangle right-0"></div>
                <div class="flex text-xs text-hex-fff items-center justify-center ml-1">相关信息</div>
            </div>
            <div class="text-xs p-3">
                <div class="flex mb-2">主持人：host</div>
                <div class="flex mb-2">准备单位：preparationUnit</div>
                <div class="flex">参加单位或人员：participants</div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router'
import { onMounted, reactive } from "vue";
const route = useRoute()
let data = JSON.parse(route.query.data)
onMounted(() => {
    console.log(data, '传过来的数据')
})
</script>

<style scoped>
.dashed-line {
    width: 1px;
    height: 5rem;
    border-left: 3px dashed blue;
    margin: 0 auto;
}

.rectangle {
    width: 70px;
    /* Set the width of the rectangle */
    height: 30px;
    /* Set the height of the rectangle */
    background-color: #5F9CEF;
    /* Set the background color of the rectangle */
    position: relative;

}

.triangle {
    border-width: 15px;
    border-style: solid;
    border-color: transparent white transparent transparent;
}
</style>