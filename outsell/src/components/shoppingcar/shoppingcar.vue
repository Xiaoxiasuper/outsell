<template>
    <div class="shoppingcar">
      <div class="content">
        <div class="leftcontent">
          <div class="logo-wrapper">
            <div class="logo">
              <div class="icon-shopping_cart"></div>
            </div>
          </div>
          <div class="countprice">0</div>
          <div class="deliveryPrice">另需配送费2元</div>
        </div>
        <div class="rightcontent">
          <div class="minPrice">2元起送</div>
        </div>
      </div>
    </div>
</template>

<script type="text/ecmascript-6">
  export default {};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shoppingcar
    position :fixed
    bottom :0
    left:0
    height:48px
    width :100%
    background :#141d27
    font-size :0
    .content
      display:flex
      .leftcontent
        flex:1
        .logo-wrapper
          position: relative
          display :inline-block
          top:-10px
          margin :0 12px 2px 12px
          padding :6px
          width: 56px
          height :56px
          border-radius :50%
          box-sizing : border-box
          background :#141d27
          text-align :center
          .logo
            width: 100%
            height :100%
            border-radius :50%
            background :rgba(255,255,255,0.2)
            .icon-shopping_cart
              font-size :24px
              line-height: 44px
              color:rgba(255,255,255,0.4)
        .countprice
          display :inline-block
          vertical-align :top
          margin-top :12px
          font-size :16px
          font-weight :700
          color:rgba(255,255,255,0.4)
          line-height :24px
          padding-right :12px
          border-right :1px solid rgba(255,255,255,0.4)
      .rightcontent
        flex:0 0 105px
        width:105px
  </style>
