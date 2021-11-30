<template>
    <v-footer app color="white" id="shopping-car-footer">
        <v-row style="margin: 0;">
            <v-col cols="3">
                <v-checkbox
                        class="flex align-center"
                        label="全选"
                        dense
                        hide-details
                        :input-value="isFull"
                        @change="fullChange" style="margin: 0;padding: 0"/>
            </v-col>
            <v-col cols="5" class="text-center red--text">
                合计：￥{{ amount.toFixed(2) }}
            </v-col>
            <v-col cols="4" class="text-right">
                <v-btn bottom outlined plain color="blue darken-4" small absolute right>
                    结算（{{ all }}）
                </v-btn>
            </v-col>
        </v-row>

    </v-footer>
</template>

<script>
    export default {
        props: {
            // 是否全选
            isFull: {
                type: Boolean,
                default: true
            },
            // 总价格
            amount: {
                default: 0,
                type: Number
            },
            // 总数量
            all: {
                type: Number,
                default: 0
            }
        },
        data() {
            return {
                isc: true
            }
        },
        // 方法
        methods: {
            /**
             * 当全选复选框发生值改变时
             * @param isChecked 修改后的状态【true\false】
             */
            fullChange(isChecked) {
                this.$emit('full-change', isChecked)
            }
        }
    }
</script>

<style lang="less" scoped>

    #shopping-car-footer {
        box-shadow: 0 -2px 2px 2px gainsboro;
    }
</style>
