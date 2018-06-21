<template>
    <div class="left-nav pull-left">
        <ul class="">
            <li>
                <i class="icon iconfont icon-wodezichan"></i>
                <div>收银</div>
            </li>
            <li>
                <i class="icon iconfont icon-31dianpu"></i>
                <div>店铺</div>
            </li>
            <li>
                <i class="icon iconfont icon-liwu"></i>
                <div>商品</div>
            </li>
            <li>
                <i class="icon iconfont icon-huiyuanqia"></i>
                <div>会员</div>
            </li>
            <li>
                <i class="icon iconfont icon-tongji"></i>
                <div>统计</div>
            </li>
            <li>
                <i class="icon iconfont icon-31shezhi"></i>
                <div>设置</div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "leftNav"
    }
</script>

<style>
.pull-left{
    float: left;
}
.left-nav li{
    list-style:none;
    background: #2b81af;
    text-align: center;
    color: #fff;
    font-size: 15px;
    height: 100%;
    padding: 15px 0;
}
.left-nav{
    overflow: hidden;
    width: 5%;
}
.left-nav ul{
    margin: 0;
    padding: 0;
}
</style>