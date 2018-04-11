<template>
    <div class="goods">
      <div class="menu-warpper">
        <div  class="name-warpper border-1px" v-for="item in goods" :key="item.id">
          <div class="name ">
            <span class="icon" :class="classMap" v-show="item.type>0"></span>{{item.name}}
          </div>
        </div>
      </div>
      <div class="foods-warpper">
        <ul v-for="good in goods" :key="good.id">
          <li class="title">{{good.name}}</li>
          <ul >
            <li class="foods-warpper" v-for="food in good.foods" :key="food.id">
              <div class="food border-1px">
                <div class="icon">
                  <img :src="food.icon"  width="64" height="64">
                </div>
                <div class="content">
                  <div class="name">{{food.name}}</div>
                  <div class="description" v-if="food.description">{{food.description}}</div>
                  <div class="condition">
                    <span class="sellCount">月售{{food.sellCount}}份</span><span class="rating">好评率{{food.rating}}%</span>
                  </div>
                  <div class="price">
                    <span class="nowprice">￥<span class="rmb">{{food.price}}</span></span>
                    <span class="oldPrice" v-if="food.oldPrice">￥<span class="rmb">{{food.oldPrice}}</span></span>
                  </div>
                </div>
                <div class="addfood">
                  <span   class="icon-remove_circle_outline"></span>
                  <span ></span>
                  <span @click="add" class="icon-add_circle"></span>
                </div>
              </div>
            </li>
          </ul>
        </ul>
      </div>
    </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0;

  export default {
    props: {
      seller:{
        type:Object
      }
    },
    data () {
      return {
        goods:{}
      };
    },
    methods: {
      add () {
        console.log(this);
      }
    },
    created: function () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];

      this.$http.get('/api/goods').then(response => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = response.data;
        }
      });
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../commen/stylus/mixim"

  .goods
    display:flex
    position :absolute
    width :100%
    top:174px
    bottom:58px
    overflow :hidden
    .menu-warpper
      flex:0 0 80px
      width :80px
      background: #f3f5f7
      overflow :auto
      .name-warpper
        margin-left :12px
        width :56px
        height :54px
        border-1px(rgba(7,17,27,0.1))
        display:flex;
        align-items:center;
        .name
          font-size :12px
          color:rgb(77,85,93)
          font-weight:200
          line-height:14px
          .icon
            vertical-align :top
            display: inline-block
            height: 12px
            width: 12px
            margin-right :4px
            &.decrease
              bg-image("decrease_3")
              background-size : 12px 12px
            background-repeat :no-repeat
            &.discount
              bg-image("discount_3")
              background-size : 12px 12px
              background-repeat :no-repeat
            &.invoice
              bg-image("invoice_3")
              background-size : 12px 12px
              background-repeat :no-repeat
            &.guarantee
              bg-image("guarantee_3")
              background-size : 12px 12px
              background-repeat :no-repeat
            &.special
              bg-image("special_3")
              background-size : 12px 12px
              background-repeat :no-repeat
    .foods-warpper
      flex:1
      overflow :auto
      .title
        font-size :12px
        line-height: 26px
        color:rgb(147,153,159)
        padding-left :14px
        border-left :2px solid #d9dde1
        background: #f3f5f7
        height :26px
      .foods-warpper
        margin:0 18px
        font-size :0
        .food
          font-size :0
          padding:18px 0
          border-1px(rgba(7,17,27,0.1))
          .icon
            vertical-align :top
            display:inline-block
            border-radius:4px
            overflow :hidden
          .content
            display: inline-block
            font-size :10px
            margin-left :10px
            width:70%
            .name
              margin-top :2px
              color:rgb(7,17,27)
              font-size: 14px
            .condition,.description
              margin-top :8px
              color:rgb(147,153,159)
              font-size :10px
              .sellCount
                margin-right :12px
            .price
              margin-top :8px
              font-size :10px
              font-weight :normal
              .nowprice
                margin-right :8px
                color:rgb(240,20,20)
                .rmb
                  font-weight :700
                  font-size :14px
              .oldPrice
                line-height :14px
                vertical-align :top
                color:rgb(147,153,159)
                text-decoration:line-through
                .rmb
                  vertical-align :top
                  font-weight :700
          .addfood
            position:absolute
            right:0
            bottom:18px
            font-size :10px
            color:rgb(147,153,159)
            .icon-remove_circle_outline
              vertical-align: middle
              margin-right :12px
              font-size :24px
              color:rgb(0,160,220)
            .icon-add_circle
              vertical-align: middle
              margin-left :12px
              font-size :24px
              color:rgb(0,160,220)
</style>
