<template>
    <v-list-item>
        <v-list-item-action class="mr-0">
            <v-checkbox :input-value="state" :id="'ck'+id" @change="stateChange"></v-checkbox>
        </v-list-item-action>
        <v-list-item-avatar tile width="100" height="100" class="mx-3">
            <label :for="'ck'+id">
                <v-img
                        :src="pic"
                        :lazy-src="pic"
                        aspect-ratio="1"
                        class="grey lighten-2"
                >
                    <template v-slot:placeholder>
                        <v-row
                                class="fill-height ma-0"
                                align="center"
                                justify="center"
                        >
                            <v-progress-circular
                                    indeterminate
                                    color="grey lighten-5"
                            ></v-progress-circular>
                        </v-row>
                    </template>
                </v-img>
            </label>
        </v-list-item-avatar>
        <v-list-item-content id="shop-car-good-info" style=""
                             class="pt-0">
            <v-list-item-title class="pb-2">
                {{title}}
            </v-list-item-title>
            <v-list-item-subtitle>红色</v-list-item-subtitle>
            <v-container class="p">
                <div class="red--text d-inline"> ￥{{price}}</div>
                <!-- 选购数量 -->
                <slot></slot>
            </v-container>
        </v-list-item-content>
    </v-list-item>
</template>

<script>
    export default {
        props: {
            // 商品编号
            id: {
                required: true, // 必填
                type: Number, // 类型【数值】
            },
            // 商品标题
            title: {
                default: '', // 默认值 ‘’
                type: String, // 类型【字符串】
            },
            // 商品价格
            price: {
                default: 0, // 默认值 0
                type: Number, // 类型【数值】
            },
            // 商品的图片
            pic: {
                default: '', // 默认值 ‘’
                type: String, // 类型【字符串】
            },
            // 商品是否勾选
            state: {
                default: true, // 默认值 true
                type: Boolean, // 类型【布尔值】
            },
            // 商品的数量
            count: {
                type: Number,
                default: 1
            }
        },
        // 方法
        methods: {
            /**
             * 当复选框值发生改变时
             * @param isChecked 是否被选
             */
            stateChange(isChecked) {
                // 传给父组件【state-change：事件】【参数：id：当前商品编号，value：值】
                this.$emit('state-change', {id: this.id, value: isChecked})
            }
        },
        // 组件
        components: {}
    }
</script>

<style lang="less" scoped>
    #shop-car-good-info {
        height: 100px;
    }
</style>
