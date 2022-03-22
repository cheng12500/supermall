<template>
    <div class="bottom-bar">
        <div class="check-content">
        <check-button 
        :is-checked="isSelectAll" 
        class="check-button" @click.native="checkClick"></check-button>
        <span>全选</span>
        </div>

        <div class="price">
            合计:{{totalPrice}}
        </div>

        <div class="calculate" @click="calcClick">
            去计算:({{checkLength}})
        </div>
    </div>
</template>

<script>
import CheckButton from 'components/content/checkButton/CheckButton'

import { mapGetters } from 'vuex'

export default {
    name:"CartBottomBar",
    components:{
        CheckButton
    },
    computed:{
        ...mapGetters(['cartList']),
        totalPrice(){
            return  '￥' +this.$store.state.cartList.filter(item=>{
                return item.checked
            }).reduce((preValue,item)=>{
                return preValue + item.price * item.count
            },0).toFixed(2)
        },
        checkLength(){
            return this.cartList.filter(item=>item.checked).length
        },
        isSelectAll(){
            // 使用filter
            // if(this.cartList.length === 0) return false
            // return !(this.cartList.filter(item=>!item.checked).length)

            // 使用find
            // if(this.cartList.length===0) return false
            // return !this.cartList.find(item=> !item.checked)

            // 普通遍历
            if(this.cartList.length===0) return false
            for(let item of this.cartList){
                if(!item.checked){
                    return false
                }
            }
            return true
        }
    },
    methods:{
        checkClick(){
            // console.log('-------');
            if(this.isSelectAll){ //全选选中
                this.cartList.forEach(item => item.checked = false)
            }else{  //部分或全部不选中
                this.cartList.forEach(item=>item.checked = true)
            }
        },
        calcClick(){
            if(!this.isSelectAll) {
                this.$toast.show('请选择购买的商品',2000)
            }
        }
    }
}
</script>

<style scoped>
    .bottom-bar{
        height: 40px;
        background-color: #eee;
        position: relative;
        line-height: 40px;
        display: flex;
    }
    .check-content{
        display: flex;
        align-items: center;
        margin-left: 10px;
        widows: 60px;
    }

    .check-button{
        width: 20px;
        height: 20px;
        line-height: 20px;
        margin-right: 5px;
    }
    .price{
        margin-left: 20px;
        flex: 1;
    }
    .calculate{
        width: 90px;
        background: red;
        color: #fff;
        text-align: center;
    }
</style>