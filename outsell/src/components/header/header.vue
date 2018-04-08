<template>
  <div class="header">
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div class="content-warpper">
      <div class="avatar">
        <img width="64" height="64"  :src="seller.avatar" >
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}} / {{seller.deliveryTime}}分钟送达
        </div>
        <div class="supports" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
        <div v-if="seller.supports" class="support-count" @click="showDetail">
          <span class="count">{{seller.supports.length}}个</span>
          <span class="icon-keyboard_arrow_right"></span>
        </div>
      </div>
    </div>
    <div class="bulletin-warpper">
      <span class="bull"></span>
      <span class="bulletin">{{seller.bulletin}}</span>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <transition name="fade">
      <div class="detail" v-show="detailShow" >
        <div class="detail-warpper clearfix">
          <div class="detail-main">
            <div class="name">{{seller.name}}</div>
            <v-star :score="seller.score" :size=48 ></v-star>
            <div class="line-warpper">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <div class="supports-warpper">
              <div class="support" v-if="seller.supports" v-for="support in seller.supports" :key="support.id">
                <span class="icon" :class="classMap[support.type]"></span>
                <span class="text">{{support.description}}</span>
              </div>
            </div>
            <div class="line-warpper">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              {{seller.bulletin}}
            </div>
          </div>
        </div>
        <div class="detail-close">
          <i class="icon-close" @click="showDetail"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star';

  export default {
    props:{
      seller:{
        type:Object
      }
    },
    data () {
      return {
        detailShow:false
      };
    },
    methods: {
      showDetail () {
        this.detailShow = !this.detailShow;
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components:{
      'v-star':star
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../commen/stylus/mixim.styl"

  .header
    position :relative
    color: #ffffff
    font-size :0
    background:rgba(7,17,27,0.5)
    overflow:hidden
    .background
      position :absolute
      z-index :-1
      top:0
      left :0
      width :100%
      height:100%
      filter:blur(10px)
    .content-warpper
      position:relative
      padding:24px 12px 18px 24px
      .avatar
        display:inline-block
        margin-right :16px
        vertical-align :top
        border-radius:4px
        overflow :hidden
      .content
        display:inline-block
        .title
          margin:2px 0 8px
          .brand
            vertical-align :top
            display:inline-block
            width :30px
            height:18px
            bg-image("brand")
            background-size :30px 18px
            background-repeat :no-repeat
          .name
            margin-left :6px
            font-size:18px
            font-weight :bold
        .description
          margin-bottom :10px
          font-size :12px
        .supports
          margin-bottom :2px
          .text
            font-size :10px
            line-height :12px
          .icon
            vertical-align :top
            display: inline-block
            height: 12px
            width: 12px
            margin-right :4px
            &.decrease
              bg-image("decrease_1")
              background-size : 12px 12px
            background-repeat :no-repeat
            &.discount
              bg-image("discount_1")
              background-size : 12px 12px
              background-repeat :no-repeat
            &.invoice
              bg-image("invoice_1")
              background-size : 12px 12px
              background-repeat :no-repeat
            &.guarantee
              bg-image("guarantee_1")
              background-size : 12px 12px
              background-repeat :no-repeat
            &.special
              bg-image("special_1")
              background-size : 12px 12px
              background-repeat :no-repeat
      .support-count
        position :absolute
        right :12px
        bottom :11px
        padding:0px 8px
        height :24px
        background-color :rgba(0,0,0,0.2)
        font-size :10px
        border-radius:14px
        .count
          vertical-align :top
          line-height :24px
          padding-right :2px
        .icon-keyboard_arrow_right
          line-height :24px
    .bulletin-warpper
      position :relative
      height :28px
      line-height :28px
      padding : 0 20px 0 12px
      overflow :hidden
      white-space:nowrap
      text-overflow :ellipsis
      font-size :10px
      background-color :rgba(7,17,27,0.2)
      .bull
        vertical-align :top
        margin-top:7px
        display: inline-block
        height :12px
        width: 22px
        bg-image("bulletin")
        background-size :22px 12px
        background-repeat :no-repeat
      .bulletin
        margin:0 4px
        line-height:28px
      .icon-keyboard_arrow_right
        position :absolute
        right: 12px
        line-height:28px

    .detail
      position:fixed
      z-index :4
      width:100%
      height:100%
      top:0
      left:0
      background-color :rgba(7,17,27,0.8)
      backdrop-filter:blur(10px)
      overflow :auto
      &.fade-enter-active, &.fade-leave-active
        transition:all 0.5s
      &.fade-enter, &.fade-leave-to
        opacity :0
        background-color :rgba(7,17,27,0)
      .detail-warpper
        min-height :100%
        width :100%
        .detail-main
          padding-bottom :64px
          margin-top: 64px
          font-size :20px
          width :100%
          .name
            font-size :16px
            font-weight :700
            text-align :center
          .star
            margin:16px auto 0 auto
            text-align :center
          .line-warpper
            display:flex
            margin:28px auto 24px auto
            width :85%
            .line
              position: relative
              flex : 1
              top: -6px
              border-bottom :1px solid rgba(255,255,255,0.2)
            .text
              font-size :14px
              font-weight :700
              margin :0 12px
          .supports-warpper
            font-size :0px
            width:75%
            margin :0 auto
            .support
              margin-bottom:12px
              .text
                font-size:12px
                line-height :16px
              .icon
                vertical-align :top
                display: inline-block
                height: 16px
                width: 16px
                margin-right :6px
                &.decrease
                  bg-image("decrease_2")
                  background-size : 16px 16px
                  background-repeat :no-repeat
                &.discount
                  bg-image("discount_2")
                  background-size : 16px 16px
                  background-repeat :no-repeat
                &.invoice
                  bg-image("invoice_2")
                  background-size : 16px 16px
                  background-repeat :no-repeat
                &.guarantee
                  bg-image("guarantee_2")
                  background-size : 16px 16px
                  background-repeat :no-repeat
                &.special
                  bg-image("special_2")
                  background-size : 16px 16px
                  background-repeat :no-repeat
          .bulletin
            width:75%
            margin :0 auto
            font-size:12px
            line-height 24px
      .detail-close
        position :relative
        height :32px
        width :32px
        margin:-64px auto 0 auto
        clear:both
        font-size :32px



</style>
