<template>
    <div class="pos">
        <div>
            <el-row >
                <el-col :span='7' class="order-list" id="order-list">
                    <el-tabs>
                        <el-tab-pane label="点餐">
                            <el-table :data="tableData" border show-summary style="width: 100%" >
                                <el-table-column prop="goodsName" label="商品"  ></el-table-column>
                                <el-table-column prop="count" label="量" width="50"></el-table-column>
                                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                                <el-table-column  label="操作" width="100" fixed="right">
                                    <template slot-scope="scope">
                                        <el-button type="text" size="small" >删除</el-button>
                                        <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                                    </template>
                                </el-table-column>
                            </el-table>
                            <div class="tatol">
                                <span>总数量：{{tatolCount}}</span>
                                <span>总价格：{{tatolMoney}}</span>
                            </div>
                            <div class="pos-btn">
                                <el-button type="warning" >挂单</el-button>
                                <el-button type="danger" >删除</el-button>
                                <el-button type="success" >结账</el-button>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="挂单">挂单</el-tab-pane>
                        <el-tab-pane label="外卖">外卖</el-tab-pane>
                    </el-tabs>
                </el-col>
                <!--商品展示-->
                <el-col :span="17">
                    <div class="often-goods">
                        <div class="title">常用商品</div>
                        <div class="often-goods-list">
                            <ul>
                                <li v-for="food in oftenGoods" @click="addOrderList(food)">
                                    <span>{{ food.goodsName }}</span>
                                    <span class="o-price">￥{{ food.price }}元</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="goods-type">
                        <el-tabs>
                            <el-tab-pane label="汉堡">
                                <ul class='cookList'>
                                    <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="小食">
                                <ul class='cookList'>
                                    <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="饮料">
                                <ul class='cookList'>
                                    <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="套餐">
                                <ul class='cookList'>
                                    <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                        </el-tabs>
                    </div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    export default {
        name: "pos",
        data () {
            return {
                tableData: [],
                oftenGoods:[],
                type0Goods:[],
                type1Goods:[],
                type2Goods:[],
                type3Goods:[],
                tatolCount:0,
                tatolMoney:0
            }
        },
        created:function () {
            axios.get('http://jspang.com/DemoApi/oftenGoods.php')
                .then(response=>{
                    this.oftenGoods=response.data;
                })
                .catch(error=>{
                    alert("网络错误，请重试");
                });
            axios.get('http://jspang.com/DemoApi/typeGoods.php')
                .then(response=>{
                this.type0Goods=response.data[0];
                this.type1Goods=response.data[1];
                this.type2Goods=response.data[2];
                this.type3Goods=response.data[3];
                })
                .catch(error=>{
                        alert("网络错误，请重试");
                });
        },
        mounted:function(){
            var orderHeight=document.body.clientHeight;
            console.log(orderHeight);
            document.getElementById("order-list").style.height=orderHeight+'px';
        },
        methods:{
            addOrderList:function (goods) {
                let tatolCount = 0;
                let tatolMoney = 0;
                let isHave = false;
                //判断订单是否存在于订单列表
                for(let i=0;i<this.tableData.length;i++){
                    console.log(this.tableData[i].goodsId);
                    if(this.tableData[i].goodsId==goods.goodsId){
                        isHave = true;
                    }
                }

                //根据isHave的值来判断订单列表中是否已经有此订单
                if(isHave){
                    //存在就进行数量的添加
                    let arr = this.tableData.filter(o=>o.goodsId == goods.goodsId);
                    console.log(arr);
                    arr[0].count++;
                }else{
                    //不存在就进行商品的添加
                    let newGoods = {goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                    console.log(newGoods);
                    this.tableData.push(newGoods);
                }

                //总数量 总价格的汇总
                this.tableData.forEach((element)=>{
                    console.log(element);
                    this.tatolCount+=element.count;
                    this.tatolMoney=this.tatolMoney+(element.count*element.price);
                });
            }
        }
    }
</script>
<style>
.order-list{
    border-right: 1px solid #ddd;
    background: #fff;
}
.title{
    height: 20px;
    border-bottom:1px solid #D3DCE6;
    background-color: #F9FAFC;
    padding:10px;
    text-align: left;
}
.often-goods-list ul li{
    list-style: none;
    float:left;
    border:1px solid #E5E9F2;
    padding:10px;
    margin:5px;
    background-color:#fff;
    cursor: pointer;
}
.often-goods-list ul{
    overflow: hidden;
}
.o-price{
    color:#58B7FF;
}
.cookList{
    overflow: hidden;
    margin: 0;
    padding: 0;
}
.cookList li{
    list-style: none;
    width:23%;
    border:1px solid #E5E9F2;
    height: auot;
    overflow: hidden;
    background-color:#fff;
    padding: 2px;
    float:left;
    margin: 2px;
    cursor: pointer;
}
.cookList li span{

    display: block;
    float:left;
}
.foodImg{
    width: 40%;
}
.foodName{
    font-size: 18px;
    padding-left: 10px;
    color:brown;

}
.foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top:10px;
}
</style>