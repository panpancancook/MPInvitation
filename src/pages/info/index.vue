<template>
  <scroll-view class="info" scroll-y="true" :scroll-top="scrollTop">
    <swiper class="info-img" :autoplay="true" :indicator-dots="sw.dotShow" :current="sw.current"
            :indicator-color="sw.dotBg" :indicator-active-color="sw.dotColor">
      <swiper-item v-for="(img,index) in showList" :key="img.id" @tap="preview(showList,index)">
        <img :src="img.src" />
      </swiper-item>
    </swiper>
    <div class="info-title">
      <p>时尚棉</p>
      <button open-type="share"><img src="/static/icon/share.png">分享</button>
    </div>
    <div class="info-desc">
      <p>样布：<span class="red">￥20.00元/米</span>大货：<span class="red">￥15.00元/米</span></p>
      <p>货号：<span>￥20.00元/米</span>编号：<span>￥15.00元/米</span></p>
      <ul>
        <p>颜色：</p>
        <li v-for="(img,index) in imgList" :key="img.id" @click="choose(index)" :class="index == activeImg ? 'active' : ''">
          <img :src="img.src">
        </li>
      </ul>
    </div>
    <div class="info-property">
      <dl>
        <dt>属性</dt>
        <dd>季节：夏、秋</dd>
        <dd>色系：黄色、蓝色、繁花</dd>
      </dl>
    </div>
    <div class="info-detail">
      <dl>
        <dt>面料详情</dt>
        <dd @tap="previewImg('/static/1.png')">
          <img src="/static/1.png" />
          <span>测试</span>
        </dd>
      </dl>
    </div>
    <div class="info-reference">
      <dl>
        <dt>参考图</dt>
        <dd>
          <img src="/static/1.png" />
        </dd>
        <dd>
          <img src="/static/2.png" />
        </dd>
      </dl>
    </div>
    <div class="info-recommended" scroll-x="true">
        <p>面料推荐</p>
        <scroll-view scroll-x="true">
        <ul>
          <li v-for="(item,index) in recommendedList" :key="item.id" @click="refresh(item.id)">
            <img :src="item.src" />
            <span>{{item.name}}</span>
            <span class="price">￥{{item.price}}{{item.unit}}</span>
          </li>
        </ul>
        </scroll-view>
    </div>
    <div class="info-ad">
      <img src="/static/1.png">
    </div>
    <!--浮动按钮-->
    <button class="po-btn page-index" @click="switchTab(1)">
        <img src="/static/icon/index-icon.png">
        <p>首页</p>
    </button>
    <button class="po-btn page-card" @click="switchTab(2)">
      <img src="/static/icon/phone-icon.png">
      <p>联系我们</p>
    </button>
  </scroll-view>
</template>

<script>
  export default{
    data () {
      return {
        sw: {
          current: 0,
          dotShow: true,
          dotBg: 'rgba(255,255,255,0.7)',
          dotColor: '#ffffff'
        },
        imgList: [
          {
            id: 1,
            src: '/static/1.png',
            children: [
              {
                id: 1,
                src: '/static/1.png'
              },
              {
                id: 2,
                src: '/static/2.png'
              }
            ]
          },
          {
            id: 3,
            src: '/static/2.png',
            children: [
              {
                id: 3,
                src: '/static/2.png'
              }
            ]
          }
        ],
        recommendedList: [
          {
            id: 1,
            src: '/static/1.png',
            name: '时尚棉',
            price: '123.00',
            unit: '元/米'
          },
          {
            id: 2,
            src: '/static/2.png',
            name: '时尚棉',
            price: '123.00',
            unit: '元/米'
          }
        ],
        showList: [],
        activeImg: 0,
        scrollTop: 0
      }
    },
    created () {
      this.showList = this.imgList[this.activeImg].children
    },
    mounted () {
      wx.setNavigationBarTitle({
        title: '面料详情'
      })
    },
    methods: {
      choose: function (index) {
        this.activeImg = index
        this.showList = this.imgList[index].children
        this.showList.length === 1 ? this.sw.dotShow = false : this.sw.dotShow = true
        this.sw.current = 0
      },
      refresh: function (id) {
        wx.redirectTo({
          url: '/pages/info/main?id=' + id,
          success: function (e) {
            console.log(e)
          },
          fail: function (e) {
            console.log(e)
          }
        })
      },
      switchTab: function (index) {
        let _url = ''
        switch (index) {
          case 1:
            _url = '/pages/store/main'
            break
          case 2:
            _url = '/pages/card/main'
            break
          default:
            _url = '/pages/store/main'
            break
        }
        wx.switchTab({
          url: _url,
          success: function (e) {
            console.log(e)
          },
          fail: function (e) {
            console.log(e)
          }
        })
      },
      preview: function (list, index) {
        let _urls = []
        for (let item of list) {
          _urls.push(item.src)
        }
        // 单张图片预览
        wx.previewImage({
          current: _urls[index],
          urls: _urls
        })
      },
      previewImg: function (src) {
        wx.previewImage({
          urls: [src]
        })
      }
    }
  }
</script>

<style lang="less" scoped>
  .info{
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
    width: 100%;
    height: 100vh;
    position: relative;
    margin: 0;
  }

  .info-img{
    width: 100%;
    height: 500rpx;
    box-shadow: 0 10rpx 10rpx #cccccc;

    img{
      width: 100%;
      height: 100%;
    }
  }

  .info-title{
    width: 100%;
    height: 60rpx;
    margin: 40rpx 0 0 0;
    padding: 0 40rpx;
    box-sizing: border-box;
    display: flex;
    justify-content: space-between;
    align-items: center;

    p{
      font-size: 35rpx;
      font-weight: bold;
    }

    button{
      display: flex;
      align-items: center;
      font-size: 28rpx;
      color: #8a8a8a;
      background: none;
      margin: 0;
      padding: 0;
      line-height: normal;

      &::after{
         border: 0;
      }
    }

    img{
      display: block;
      height: 30rpx;
      width: 30rpx;
      margin: 0 10rpx 0 0;
    }
  }

  .common-div{
    width: 100%;
    padding: 30rpx 40rpx;
    border-bottom: 2rpx solid #eeeeee;
    display: flex;
    flex-wrap: wrap;
    box-sizing: border-box;
  }
  .common-dl{
    dl{
      width: 100%;
      display: flex;
      flex-wrap: wrap;

      dt{
        width: 100%;
        font-size: 35rpx;
        font-weight: bold;
        margin: 0 0 20rpx 0;
      }
    }
  }

  .info-desc{
    .common-div;
    .common-dl;
    p{
      display: flex;
      width: 100%;
      font-size: 28rpx;
      color: #999999;
      margin: 0 0 10rpx 0;
    }

    span{
      display: block;
      width: 230rpx;
    }
    .red{
      color: #fc0c0a;
    }

    ul{
      display: flex;
      width: 100%;
      margin: 10rpx 0 0 0;
      list-style: none;
      font-size: 28rpx;
      color: #999999;

      p{
        width: 100rpx;
        margin: 0 10rpx 0 0;
      }

      li{
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0 20rpx 0 0;
        width: 80rpx;
        height: 80rpx;
        box-sizing: border-box;
      }
      .active{
        border: 1rpx solid #fc0c0a;
      }

      img{
        width: 76rpx;
        height: 76rpx;
      }
    }
  }

  .info-property{
    .common-div;
    .common-dl;
    dd{
      width: 50%;
      font-size: 28rpx;
      color: #999999;
    }
  }

  .info-detail{
    .common-div;
    .common-dl;
    dd{
      position: relative;
      box-sizing: border-box;
      width: 100%;
      height: 300rpx;
      margin: 20rpx 0 0 0;

      img{
        width: 100%;
        height: 100%;
        border-radius: 50rpx;
        border: 3rpx solid #eeeeee;
        box-sizing: border-box;
      }

      span{
        position: absolute;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 50rpx;
        font-size: 28rpx;
        color: #666666;
        left: 0;
        bottom: 0;
        background: rgba(255, 255, 255, 0.7);
        border-radius: 0 0 50rpx 50rpx;
      }
    }
  }

  .info-reference{
    .common-div;
    .common-dl;
    dd{
      display: flex;
      width: 50%;
      height: 300rpx;

      img{
        width: 90%;
        height: 100%;
        border-radius: 20rpx;
        box-sizing: border-box;
        border: 3rpx solid #eeeeee;
      }
    }
  }

  .info-recommended{
    .common-div;
    p{
      width: 100%;
      font-size: 35rpx;
      font-weight: bold;
      margin: 0 0 20rpx 0;
    }

    ul{
      display: flex;

      li{
        width: 200rpx;
        margin: 0 30rpx 0 0;
        box-sizing: border-box;
        display: flex;
        flex-wrap: wrap;

        img{
          width: 200rpx;
          height: 200rpx;
        }

        span{
          width: 100%;
          font-size: 28rpx;
          color: #333333;
          margin: 10rpx 0 0 0;
        }
        .price{
          font-size: 26rpx;
          margin: 5rpx 0 0 0;
          color: #ef3e14;
        }
      }
    }
  }

  .info-ad{
    .common-div;
    justify-content: center;
    img{
      width: 90%;
    }
  }


  .po-btn{
    position: fixed;
    right: 5rpx;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 60rpx;
    height: 100rpx;
    line-height: normal;
    background: #ffffff;
    padding: 0 10rpx;
    margin: 0;

    &::after{
      border: 2rpx solid #e1e1e1;
    }

    &.page-index{
      bottom: 300rpx;
    }
    &.page-card{
       bottom: 150rpx;
    }

    p{
      width: 100%;
      font-size: 20rpx;
      color: #8a8a8a;
      text-align: center;
    }

    img{
      width: 30rpx;
      height: 30rpx;
    }
  }
</style>
