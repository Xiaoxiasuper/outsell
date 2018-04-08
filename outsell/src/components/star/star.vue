<template>
    <div :class="starType" class="star">
      <span v-for="starClass in starClasses" :class="starClass" class="star-item" :key="starClass.id"></span>
    </div>
</template>

<script type="text/ecmascript-6">

  const LENTHGT = 5;

  export default {
    props: {
      size:{
        type:Number
      },
      score:{
        type:Number
      }
    },
    computed : {
      starType () {
        return 'star' + this.size;
      },
      starClasses () {
        let result = [];
        let score = Math.floor(this.score * 2) / 2;
        let half = score % 1 !== 0;
        let demarcation = Math.floor(score);
        for (let i = 0; i < demarcation; i++) {
          result.push('star-on');
        };
        if (half) {
          result.push('star-half');
        } else {
          result.push('star-off');
        };
        for (let i = 0; i < LENTHGT - demarcation - 1; i++) {
          result.push('star-off');
        };
        return result;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../commen/stylus/mixim.styl"

  .star
    width :100%
    &.star24
      .star-item
        display :inline-block
        margin-right :2px
        width :10px
        height :10px
        &.star-on
          bg-image("star24_on")
          background-size :10px 10px
          background-repeat :no-repeat
        &.star-half
          bg-image("star24_half")
          background-size :10px 10px
          background-repeat :no-repeat
        &.star-off
          bg-image("star24_off")
          background-size :10px 10px
          background-repeat :no-repeat
    &.star36
      .star-item
        display :inline-block
        margin-right :15px
        width :15px
        height :15px
        &.star-on
          bg-image("star36_on")
          background-size :15px 15px
          background-repeat :no-repeat
        &.star-half
          bg-image("star36_half")
          background-size :15px 15px
          background-repeat :no-repeat
        &.star-off
          bg-image("star36_off")
          background-size :15px 15px
          background-repeat :no-repeat
    &.star48
      .star-item
        display :inline-block
        margin-right :16px
        width :20px
        height :20px
        &.star-on
          bg-image("star48_on")
          background-size :20px 20px
          background-repeat :no-repeat
        &.star-half
          bg-image("star48_half")
          background-size :20px 20px
          background-repeat :no-repeat
        &.star-off
          bg-image("star48_off")
          background-size :20px 20px
          background-repeat :no-repeat


</style>
