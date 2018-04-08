<template>
    <div class="goods">
      <div class="menu-warpper">
        <div class="name-warpper border-1px" v-for="item in goods" :key="item.id">
          <div class="name ">
            <span class="icon" :class="classMap" v-show="item.type>0"></span>{{item.name}}
          </div>
        </div>
      </div>
      <div class="foods-warpper"></div>
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
    created: function () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];

      this.$http.get('/api/goods').then(response => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = response.data;
          console.log(this.goods);
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

</style>
