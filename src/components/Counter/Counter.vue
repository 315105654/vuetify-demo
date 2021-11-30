<template>
    <div class="float-right">
        <v-icon x-small @click="sub">mdi-minus</v-icon>
        <span class="px-2 font-weight-bold">{{num}}</span>
        <v-icon x-small @click="add">mdi-plus</v-icon>


    </div>
</template>

<script>
    export default {
        props: {
            // 商品的编号
            id: {
                type: Number,
                require: true
            },
            // 数量
            num: {
                type: Number,
                default: 1
            }
        },
        methods: {
            add() {
                this.$emit('num-change', this.num + 1)
            },
            sub() {
                if (this.num - 1 === 0) {
                    return
                }
                this.$emit('num-change', this.num - 1)
            }
        }
    }
</script>

<style lang="less" scoped></style>
