<template>
    <div>
        <LayOut name="ToDay">
            <ShowMoney>
                <span slot="title_slot" class="title">今日支出</span>
                <span slot="pay_slot" class="pay">￥ 33</span>
                <span slot="income_slot" class="income">本月收入 ￥ 33</span>
            </ShowMoney>
            <MoneyKey/>
        </LayOut>
    </div>
</template>
<script>
    import ShowMoney from '@/components/money/ShowMoney.vue';
    import MoneyKey from '@/components/money/MoneyKey.vue';
    export default {
        components:{MoneyKey,ShowMoney},

    }
</script>
<style lang="scss" scoped>
    .money-link {
        margin: 28px auto 0;
        background-color: #A1DECF;
        font-size: 18px;
        font-weight: 700;
        border-radius: 10px;
        padding: 14px;
        max-width: 141px;
        text-align: center;
    }
</style>