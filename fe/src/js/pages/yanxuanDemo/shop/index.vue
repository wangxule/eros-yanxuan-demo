<template>
    <div class="wrapper">
        <shop-header title="购物车" :rightBtn="rightBtn"></shop-header>
        <div class="slogan" @click="jump2($event,'true')">
            <text class="i-slg iconfont">&#xe63a; 30天无忧退换货</text>
            <text class="i-slg iconfont">&#xe63a; 48小时快速退款</text>
            <text class="i-slg iconfont">&#xe63a; 满88元免邮费</text>
        </div>
        <scroller class="main-list" offset-accuracy="300px">
            <refresher></refresher>
            <div class="shop-cart">
                <div v-if="!goodList || goodList.length<=0" class="cart-empty">
                    <image class="img-empty" resize="contain" src="http://yanxuan.nosdn.127.net/hxm/yanxuan-wap/p/20161201/style/img/icon-normal/noCart-a8fe3f12e5.png"></image>
                    <text class="txt-empty">去添加点什么吧</text>
                </div>
            </div>
            <block :goods="goods"></block>
        </scroller>
    </div>
</template>
<script>
import 'Config'
import header from './header';
import block from './block';
import refresher from '../common/refresh';

export default {
    components: {
        'shop-header': header,
        'refresher': refresher,
        'block': block,
    },
    created() {
        this.getGoods()
    },
    data() {
        return {
            rightBtn: {
                name: "编辑"
            },
            goods: [],
            goodList: []
        }
    },
    methods: {
        getGoods() {
            this.$fetch({
                method: 'GET',
                name: 'yanxuan_shop_getGoods',
                data: {}
            }).then(resData => {
                this.goods = resData.data
            }, error => {

            })
        }
    }
}
</script>
<style lang="sass" src="./index.scss"></style>