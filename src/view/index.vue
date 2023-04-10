<template>
    <section class="blowup-picture">
        <section class="box" v-for="(item, index) in dataList" :key="index" :style="{ 'clip-path': item.path }">
        </section>
    </section>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted, nextTick } from 'vue'
let dataList: any = reactive([
    // 多边形
    {
        id: '1',
        list: ['543px 443px', '335px 627px', '336px 640px', '395px 642px', '582px 479px', '851px 588px', '1505px 626px', '1505px 609px', '1158px 505px', '543px 443px'],
        type: 'POLYGON',
        isClick: false,
        points: [{ x: 543, y: 443 }, { x: 335, y: 627 }, { x: 336, y: 640 }, { x: 395, y: 642 }, { x: 582, y: 479 }, { x: 851, y: 58 }, { x: 1505, y: 626 }, { x: 1505, y: 609 }, { x: 1158, y: 505 }, { x: 543, y: 443 },]
    },
    // // 圆形
    {
        id: '2',
        center: '55% 80%',
        radius: '40px',
        type: 'CIRCLE',
        isClick: false,
    },
    // 矩形
    {
        id: '3',
        marginTop: '420px',
        marginLeft: '100px',
        marginBottom: '680px',
        marginRight: '1250px',
        type: 'INSET',
        isClick: false,
    },
]);

// mounted挂载
onMounted(() => {
    nextTick(() => {
        init();
    })
})
// 初始化
const init = () => {
    dataList && dataList.length && dataList.forEach((v: any) => {
        if (v.type === 'POLYGON') {
            v.path = v.type + '(' + v.list.join(',') + ')';
            console.log('v.path', v.path);
        }
        else if (v.type === 'CIRCLE') {
            v.path = v.type + '(' + v.radius + ' at ' + v.center + ')'
            console.log('v.path', v.path);
        }
        else if (v.type === 'INSET') {
            v.path = v.type + '(' + v.marginTop + ' ' + v.marginRight + ' ' + v.marginBottom + ' ' + v.marginLeft + ')'
            console.log('v.path', v.path);
        }
    })
    window.addEventListener('click', (e) => {
        console.log(e);
    })
}

</script>

<style lang="scss" scoped>
.blowup-picture {
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
    margin: auto;
    // filter: drop-shadow(10px 10px 10px red);
    background: url('../assets/image/floor.jpg') no-repeat;
    background-size: cover;
    z-index: 100;

    .box {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        cursor: pointer;
        z-index: 999;
        background: url('../assets/image/floor.jpg') no-repeat;
        background-size: cover;

        img {

            width: 100%;
            height: 100%;
        }

        &:hover {
            transform: scale(1.05, 1.05);
            cursor: pointer;
        }
    }

}
</style>