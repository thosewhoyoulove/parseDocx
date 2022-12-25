<!--
 * @Description: 
 * @Author: 曹俊
 * @Date: 2022-12-16 17:49:11
 * @LastEditors: 曹俊
 * @LastEditTime: 2022-12-25 10:50:41
-->
<template>
    <div class=" h-100vh pt-5">
        <div v-for="(item, index) in data" :key="index">

            <div
                class="flex w-50 h-20 bg-hex-5F9CEF border rounded-xl my-0 mx-auto text-hex-fff items-center justify-center">
                {{ item.day }}
            </div>
            <div class="flex dashed-line text-center"></div>
            <div v-for="it in item?.children" class=" border border-hex-5F9CEF mx-4 my-1">
                <div
                    class="flex w-100% bg-hex-5F9CEF h-15 text-center items-center justify-center text-hex-fff font-600">
                    {{ it?.todo }}
                </div>
                <div class="text-xs p-3">
                    <div class="flex mb-2 items-center "><img class="bg-hex-5F9CEF h-5 w-5" src="../../public/time.png"
                            alt="">
                        <div class="ml-2">
                            {{ item.day.slice(6) }} {{ it?.time }}
                        </div>
                    </div>
                    <div class="flex items-center"><img class="bg-hex-5F9CEF h-5 w-5" src="../../public/space.png"
                            alt="">
                        <div class="ml-2">{{ it?.place }}</div>
                    </div>
                </div>

                <div class="flex rectangle">
                    <div class="absolute w-0 h-0 triangle right-0"></div>
                    <div class="flex text-xs text-hex-fff items-center justify-center ml-1">相关信息</div>
                </div>
                <div class="text-xs p-3">
                    <div class="flex mb-2">主持人：{{ it?.host }}</div>
                    <div class="flex mb-2">准备单位：{{ it?.preparationUnit }}</div>
                    <div class="flex text-left">参加单位或人员：{{ it?.participants }}</div>
                </div>
            </div>
        </div>
    </div>

</template>

<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router'
import { onMounted, reactive, ref } from "vue";

import { decompressFromEncodedURIComponent as decode, compressToEncodedURIComponent as encode } from 'lz-string'
const route = useRoute()
let data = JSON.parse(route.query.data)
let encodedUrl = ref()
let decodedUrl = ref()
onMounted(() => {
    console.log(data, '传过来的数据')

    encodedUrl.value = encode(window.location.search)

    decodedUrl.value = decode(encodedUrl.value)
    console.log(decodedUrl.value, 'decodedUrl.value');
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