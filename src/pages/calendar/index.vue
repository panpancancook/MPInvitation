<template>
  <div class="calendar">
    <p class="year"><i class="prev"></i>{{year}}-{{month}}<i i class="next"></i></p>
    <ul class="date">
      <li class="day title" v-for="t of dayTitle" :key="t">{{t}}</li>
      <li :class="d === currentDay ? 'day active' : 'day'" v-for="d of day" :key="d">{{d}}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        year: new Date().getFullYear(),
        month: new Date().getMonth() + 1,
        currentDay: new Date().getDate(),
        dayTitle: ['日', '一', '二', '三', '四', '五', '六'],
        day: []
      }
    },
    computed: {
    },
    created () {
      const date = new Date() // 当前时间
      const firstDay = new Date(date.getFullYear() + '-' + (date.getMonth() + 1) + '-01') // 当前月份1号
      const days = []
      let maxDay
      for (let i = 0; i < firstDay.getDay(); i++) {
        days.push('')
      }
      switch (date.getMonth() + 1) {
        case 1: case 3: case 5: case 7: case 8: case 10: case 12:
          maxDay = 31
          break
        case 4: case 6: case 9: case 11:
          maxDay = 30
          break
        case 2:
          date.getFullYear() % 4 === 0 ? maxDay = 29 : maxDay = 28
          break
        default:
          break
      }
      for (let i = 0; i < maxDay; i++) {
        days.push(i + 1)
      }
      this.day = days
    }
  }
</script>

<style lang="less" scoped>
  .calendar{
    width: 100%;
    height: 100vh;
    padding: 0 80rpx;
    overflow: hidden;
    background-color: #ffffff;
    box-sizing: border-box;

    .date{
      width: 100%;
      display: flex;
      flex-wrap: wrap;
      box-sizing: border-box;
    }

    .year{
      width: 100%;
      display: flex;
      justify-content: center;
      margin: 0 0 30rpx 0;
      box-sizing: border-box;
    }

    .day{
      height: 80rpx;
      width: 80rpx;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #333333;

      &.active{
        color: #71b2fc;
      }
      &.title{
        color: #999999;
        font-size: 30rpx;
        padding: 0 0 10rpx 0;
        margin: 0 0 20rpx 0;
        border-bottom: 3rpx solid #e1e1e1;
      }
    }
  }
</style>
