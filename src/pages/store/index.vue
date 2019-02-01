<template>
  <scroll-view class="store">
    <div class="search">
      <input placeholder="请输入面料名称/货号" />
      <icon class="search-icon" type="search" size="22"></icon>
    </div>
      <swiper class="banner" autoplay="true" duration="800" interval="5000" circular="true"
              previous-margin="50rpx" next-margin="50rpx" @change="changeStyle">
        <swiper-item v-for="(img,index) in imgList" :key="img.id">
          <div :class="img.id == bannerIndex ? 'banner-item' : 'banner-item translucence'" :ref="'item'+index">
            <img :src="img.src" />
          </div>
        </swiper-item>
      </swiper>
      <p class="title">新品面料</p>
      <div class="item" @click="gotoInfo">
        <div class="images">
          <div class="left"></div>
          <div class="right"></div>
        </div>
        <div class="content">
          <p class="name">
            时尚棉
            <ul class="tag-list">
            <li class="tag">热销</li>
            <li class="tag">新品</li>
            </ul>
          </p>
          <p class="price"><span>￥20.00</span> 元/米</p>
          <ul class="desc-list">
            <li class="desc">柔软舒适<img src="/static/good.png"></img></li>
            <li class="desc">纯棉<img src="/static/good.png"></img></li>
          </ul>
        </div>
      </div>
  </scroll-view>
</template>

<script>
  export default {
    data () {
      return {
        bannerIndex: 0,
        imgList: [{
          id: 0,
          src: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1543209535678&di=08fcecf080e824fd3d99093a8a1dc07c&imgtype=0&src=http%3A%2F%2Fpic1.win4000.com%2Fwallpaper%2Fd%2F573ff3aeae8cc.jpg'
        },
        {
          id: 1,
          src: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1542966608221&di=ceb2f1dffc141dacf9116cfff7fa9f8b&imgtype=0&src=http%3A%2F%2F5b0988e595225.cdn.sohucs.com' +
            '%2Fq_70%2Cc_zoom%2Cw_640%2Fimages%2F20180705%2Faebc87e30fe542cbac917371d3ea1abb.jpeg'
        },
        {
          id: 2,
          src: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1543209535678&di=08fcecf080e824fd3d99093a8a1dc07c&imgtype=0&src=http%3A%2F%2Fpic1.win4000.com%2Fwallpaper%2Fd%2F573ff3aeae8cc.jpg'
        }],
        items: [{
          id: 1,
          images: []
        }]
      }
    },
    computed: {
    },
    created () {
    },
    mounted () {
      wx.setNavigationBarTitle({
        title: '首页'
      })
    },
    init () {
    },
    watch: {
    },
    methods: {
      changeStyle: function (e) {
        this.bannerIndex = e.target.current
      },
      gotoInfo: function (e) {
        wx.navigateTo({
          url: '/pages/info/main',
          success: function (e) {
          }
        })
      }
    }
  }
</script>

<style lang="less" scoped>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  .store{
    width: 100%;
    margin: 0;
    display: flex;
    align-content: flex-start;
    flex-wrap: wrap;
    background-color: #eeeeee;
  }

  .search{
    width: 100%;
    height: 80rpx;
    padding: 20rpx 0 0 0;
    display: flex;
    justify-content: center;
    align-items: center;
    position: realtive;

    input{
      display: block;
      width: 80%;
      height: 80rpx;
      padding: 0 3%;
      background-color: #ffffff;
      border: 3rpx solid #e1e1e1;
      border-radius: 10rpx;
      font-size: 28rpx;
    }

    &-icon{
      position: absolute;
      display: block;
      right: 11%;
      top: 38rpx;
    }
  }

  .banner{
    width: 100%;
    height: 800rpx;
    margin: 40rpx 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;

    swiper-item{
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    &-item{
      width: 95%;
      height: 780rpx;
      border: 3rpx solid #e1e1e1;
      border-radius: 30rpx;
      background-color: #ffffff;
      box-sizing: border-box;
      box-shadow: 5rpx 7rpx 5rpx #dddddd;
      display: flex;
      justify-content: center;
      align-items: center;

      &.translucence{
         opacity: 0.5;
         height: 750rpx;
      }
    }

    img{
      display: block;
      width: 100%;
      height: 100%;
      border-radius: 30rpx;
    }
  }

  .title{
    font-size: 40rpx;
    font-weight: bold;
    margin: 50rpx 0 30rpx 12%;
  }

  .item{
    width: 100%;
    height: 800rpx;
    margin: 0 0 50rpx 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    box-sizing: border-box;

    .images{
      width: 80%;
      height: 600rpx;
      background-color: #ffffff;
      border-radius: 20rpx 20rpx 0 0;
      border: 1rpx solid #eeeeee;
      box-sizing: border-box;
      background-color: #e1e1e1;
      box-sizing: border-box;
    }
    .left{
      width: 64%;
      height: 100%;
      margin: 0 1% 0 0;
      display: flex;
      justify-content: center;
      box-sizing: border-box;

      img{
        max-width: 100%;
        max-height: 100%;
      }
    }
    .right{
      width: 35%;
      height: 100%;
      display: flex;
      flex-wrap: wrap;
      box-sizing: border-box;

      img{
        width: 100%;
      }
    }

    .content{
      width: 80%;
      height: 200rpx;
      padding: 20rpx 30rpx;
      border-radius: 0 0 20rpx 20rpx;
      background-color: #ffffff;
      display: flex;
      align-content: flex-start;
      align-items: flex-start;
      flex-wrap: wrap;
      box-sizing: border-box;

      .name{
        width: 100%;
        font-size: 35rpx;
        font-weight: bold;
        display: flex;
        align-items: center;
        justify-content: space-between;
        position: relative;
        box-sizing: border-box;

        .tag-list{
          list-style: none;
          display: flex;
        }

        .tag{
          height: 40rpx;
          margin: 0 0 0 15rpx;
          padding: 0 15rpx;
          line-height: 40rpx;
          font-size: 28rpx;
          color: #fb7033;
          border: 2rpx solid #fca67f;
          border-radius: 20rpx;
        }
      }

      .price{
        width: 100%;
        margin: 10rpx 0 0 0;
        font-size: 30rpx;

        span{
          font-size: 35rpx;
          color: #e43d30;
        }
      }

      .desc-list{
        width: 100%;
        margin: 10rpx 0 0 0;
        list-style: none;
        display: flex;

        .desc{
          display: flex;
          align-items: center;
          height: 40rpx;
          color: #f0394e;
          font-size: 25rpx;
          margin: 0 15rpx 0 0;
          padding: 0 15rpx;
          border-radius: 18rpx;
          background-color: #feeeca;

          img{
            display: block;
            width: 25rpx;
            height: 25rpx;
            margin: 0 0 0 5rpx;
          }
        }
      }
    }
  }
</style>
