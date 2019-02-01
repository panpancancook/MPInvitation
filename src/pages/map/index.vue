<template>
  <div class="map">
    <map id="storeMap" class="map" :longitude="longitude" :latitude="latitude" scale="18" bindcontroltap="controltap"
         markers="" bindmarkertap="markertap" bindregionchange="regionchange" show-compass="true" show-location="true">
      <cover-view class="view">
        <cover-image class="cover-img" src="/static/location.png" />
      </cover-view>
    </map>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        mapTxt: '',
        longitude: 113.324520,
        latitude: 23.099094
      }
    },
    created () {
    },
    mounted () {
      wx.setNavigationBarTitle({
        title: '店铺位置'
      })

      this.mapTxt = wx.createMapContext('myMap')
      console.log(this.mapTxt)
    }
  }
</script>

<style lang="less" scoped>
  .map{
    width: 100%;
    height: 100vh;
  }

  .view{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 80rpx;
    height: 80rpx;
    left: 45%;
    top: 40%;
    position: absolute;
  }

  .cover-img{
    width: 80rpx;
    height: 80rpx;
  }
</style>
