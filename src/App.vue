<template>
    <v-app id="inspire">
        <Header></Header>
        <v-main>
            <v-list dense>
                <Goods
                        v-for="item in list"
                        :key="item.id"
                        :id="item.id"
                        :title="item.goods_name"
                        :pic="item.goods_img"
                        :price="item.goods_price"
                        :count="item.goods_count"
                        :state="item.goods_state"
                        @state-change="getChangeGoodsState"
                >
                    <Counter :num="item.goods_count" @num-change="getNewNum(item,$event)"></Counter>
                </Goods>
            </v-list>
        </v-main>
        <Footer
                :is-full="fullState"
                :amount="amt"
                :all="total"
                @full-change="getFullChange"
        ></Footer>
    </v-app>
</template>

<script>
    import Goods from "./components/Goods/Goods";
    import Header from "./components/Header/Header";
    import Footer from "./components/Footer/Footer";
    import Counter from "./components/Counter/Counter";

    export default {
        data: () => ({
            list: [], // 商品集合
        }),
        // 方法
        methods: {
            // 请求获取商品
            async initCartList() {
                const {data: res} = await axios.get('https://www.escook.cn/api/cart');
                // 请求成功 --> 获取商品list
                if (res.status === 200) {
                    this.list = res.list;
                }
            },
            /**
             * 商品勾选状态发生改变
             * @param e 改变后传过来的值 {id:Number, value:Boolean}
             */
            getChangeGoodsState(e) {
                // 依次判断改的是哪一个商品
                this.list.some(item => {
                    if (item.id === e.id) {
                        // 更改符合条件商品的 goods_state 的值为 value
                        item.goods_state = e.value
                        return true;
                    }
                })
            },
            /**
             * 商品全选勾选状态发生改变
             * @param value 改变后传过来的值 value
             */
            getFullChange(value) {
                this.list.forEach(item => item.goods_state = value)
            },
            /**
             * 改变商品的数量
             * @param item 当前商品对象
             * @param numValue 数量值
             */
            getNewNum(item, numValue) {
                // 修改该商品的数量
                item.goods_count = numValue
            }
        },
        // 计算属性
        computed: {
            // 动态计算出全选的状态
            fullState() {
                return this.list.every(item => item.goods_state)
            },
            // 勾选商品的总价
            amt() {
                return this.list
                    .filter(item => item.goods_state)
                    .reduce((total, item) => {
                        return total += item.goods_price * item.goods_count
                    }, 0)
            },
            // 勾选的数量
            total() {
                return this.list.filter(item => item.goods_state).reduce((t, item) => {
                    return t += item.goods_count
                }, 0)
            }
        },
        created() {
            this.initCartList()
        },
        // 注册组件
        components: {
            Header,
            Footer,
            Goods,
            Counter
        }
    }
</script>