<template>
    <div class="alipay">
        <order-header title="订单支付">
            <template v-slot:tip>
                <span>请谨防钓鱼链接或诈骗电话，了解更多></span>
            </template>
        </order-header>
        <loading v-if="loading"></loading>
        <div class="form" v-html="content"></div>
    </div>
</template>

<script>
    import OrderHeader from 'components/OrderHeader'
    import Loading from 'components/Loading'
    export default {
        name: 'alipay',
        data() {
            return {
                orderId:this.$route.query.orderId,
                content: '',
                loading: true
            }
        },
        mounted() {
            this.paySubmit()
        },
        methods: {
            async paySubmit() {
                const res = await this.axios.post('/pay', {
                    orderId:this.orderId,
                    orderName:'Vue高仿小米商城',
                    amount:0.01,//单位元
                    payType:1 //1支付宝，2微信
                })

                this.content = res.content
                setTimeout(() => {
                    document.forms[0].submit()
                }, 100)
            }
        },
        components:{
            Loading,
            OrderHeader
        }
    }
</script>

<style lang="scss" scoped>

</style>