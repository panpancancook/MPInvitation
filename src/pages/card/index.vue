<template>
  <div class="card">
    <div class="card-content">
      <div class="card-head">
        <img src="/static/icon/logo.png">
        <div class="right">
          <p class="name">同益纺织</p>
          <p class="desc">主营时尚布匹</p>
        </div>
      </div>
      <p class="detail"></p>
      <ul>
        <li @click="navigateToMap"><img src="/static/icon/map-icon.png">地址</li>
        <li @click="phoneCall"><img src="/static/icon/call-icon.png">电话</li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      userInfo: {}
    }
  },
  components: {
  },
  mounted () {
    wx.setNavigationBarTitle({
      title: '店铺名片'
    })
  },
  methods: {
    navigateToMap: (e) => {
      wx.navigateTo({
        url: '/pages/map/main'
      })
    },
    phoneCall: (e) => {
      wx.makePhoneCall({
        phoneNumber: ''
      })
    }
  }
}
</script>

<style lang="less" scoped>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .card{
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    align-content: center;
    justify-content: center;
    background: url("https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1543404367510&di=3130dc38022ee4bb2edbcbb219962d6b&imgtype=0&src=http%3A%2F%2Fimg02.tooopen.com%2Fimages%2F20150530%2Ftooopen_sy_127217482155.jpg") repeat;
  }

  .card-content{
    position: relative;
    width: 90%;
    height: 500rpx;
    margin: 300rpx 0 0 0;
    padding: 30rpx 40rpx;
    border-radius: 40rpx;
    background-color: rgba(255,255,255,0.7);
    box-sizing: border-box;

    p{
      width: 100%;
    }

    .card-head{
      display: flex;
      align-items: center;
      width: 100%;
      height: 80rpx;

      img{
        width: 80rpx;
        height: 80rpx;
        border-radius: 30rpx;
        margin: 0 20rpx 0 0;
      }

      .name{
        font-size: 36rpx;
        font-weight: bold;
        margin: 0 0 5rpx 0;
      }
      .desc{
        font-size: 25rpx;
      }
    }

    .detail{
      text-indent: 30rpx;
      font-size: 25rpx;
      color: #666666;
      margin: 20rpx 0;
    }

    ul{
      position: absolute;
      bottom: 0;
      left: 0;
      box-sizing: border-box;
      padding: 40rpx 40rpx;
      width: 100%;
      display: flex;
      justify-content: center;
      list-style: none;

      li{
        display: flex;
        align-items: flex-end;
        font-size: 32rpx;
        color: #999999;
        border-right: 5rpx solid #dddddd;
        box-sizing: border-box;
        padding: 0 30rpx;

        img{
          width: 50rpx;
          height: 50rpx;
          margin: 0 10rpx 0 0;
        }

        &:last-child{
          border-right: 0;
        }
      }
    }
  }
</style>
