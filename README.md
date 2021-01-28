# 项目：衣家悦商城首页实现精简交互的技术实现
## 功能介绍
  将精简交互融入到商品预览，实现商品的主动推送。类似于短视频交互，用户通过上下滑动界面，实现商品的切换，并且会有智能提示引导用户操作，点击商品大图会跳转到相对应的商品详情页。
## 功能效果
  eg：![功能效果图](https://raw.githubusercontent.com/simplenetes/YIJIAYUE/edit/main/image.png)
## index.wxml
````
<!--swiper实现整屏划动播放视频-->
<swiper vertical duration="200" bindchange="slide" style="height:{{screenHeight}}px; width:100%;background:#000;">
  <block wx:for="{{goodsPic}}" wx:key="id">
    <swiper-item style="height:100%; width:100%">

      <!--商品图片-->
      <image bindtap="toDetail" src="{{item.url}}" class="bigPic"></image>

      <!--引导教程-->
      <view hidden="{{teachFlag2}}" animation="{{animationMiddleHeaderItem}}">
        <image hidden="{{teachFlag2}}" class="teachit2" src="/pic/icon/slide.png"></image> 
        <view hidden="{{teachFlag2}}" class="clickitit2"></view>
      </view>
      <view hidden="{{teachFlag1}}" animation="{{animationMiddleHeaderItem2}}" bindtap="clikefromhere">
        <image hidden="{{teachFlag1}}" class="teachit" src="/pic/icon/teachit.png"></image> 
        <view hidden="{{teachFlag1}}" class="clickitit">进入详情页</view> 
      </view>

      <!-- 商家logo组件 -->
      <image id="model" src="../../pic/home/model.jpg"></image>
      <image id="modelImg" bindtap="toShop" hidden="{{false}}" src="../../pic/home/modelImg.png"></image>

      <!-- 点赞 -->
      <image bindtap="like" hidden="{{unlikeHidden}}" src="../../pic/home/like.png" id="like"></image>
      <image bindtap="unlike" hidden="{{likeHidden}}" src="../../pic/home/likeSelected.png" id="like"></image>
      <!-- 分享 -->
      <image src="../../pic/home/share.png" id="share"></image>
      <button id="share2" open-type="share"></button>

      <!-- 点赞数 -->
      <text animation="{{likeNumAnm}}" id="num_like">{{likenum}}</text>
      <!-- 分享数 -->
      <text id="num_share">{{sharenum}}</text>

      <!-- 评论滚动显示组件 -->
      <view class="msg-box">
        <view class="msg-swiper">
          <swiper class="msg-swiper-scroll" circular="true" autoplay="true" interval="2200" duration="700" vertical="true">
            <swiper-item wx:for="{{scrollMsg}}" wx:key="index">
              <image class="scroll-avatar" src="{{item.avatar}}"></image>
              <view class="msg-text">{{item.nickName}}：{{item.content}}</view>
            </swiper-item>
          </swiper>
          <view class="scroll-msg-cover"></view>
        </view>
      </view>
    </swiper-item>

  </block>

</swiper>
````

## index.wxss
````
page {
  height: 100%;
  overflow: hidden;
}

/*评论滚动组件*/
.msg-box {
  position: absolute;
  height: 70rpx;
  width: 600rpx;
  margin-top: 1020rpx;
  margin-left: 55rpx;
}

.teachit{
  position: absolute;
  width: 200rpx;
  height: 200rpx;
  margin-top: 570rpx;
  margin-left: 270rpx;
  z-index: 999;
}

.teachit2{
  position: absolute;
  width: 200rpx;
  height: 200rpx;
  margin-top: 615rpx;
  margin-left: 270rpx;
  z-index: 999;
}

.clickitit{
  position: absolute;
  width: 250rpx;
  height: 250rpx;
  margin-top: 510rpx;
  margin-left: 250rpx;
  font-size: x-large;
  padding-left: 20rpx;
  color: rgb(201, 201, 201);
  background-color: rgba(221, 221, 221, 0.199);
  border-radius: 10%;
  z-index: 999;
} 

.clickitit2{
  position: absolute;
  width: 250rpx;
  height: 250rpx;
  margin-top: 590rpx;
  margin-left: 250rpx;
  font-size: x-large;
  padding-left: 20rpx;
  color: rgb(165, 165, 165);
  background-color: rgba(221, 221, 221, 0.199);
  border-radius: 10%;
  z-index: 999;
} 

/*评论滚动组件 swiper*/
.msg-swiper {
  border-radius: 5%;
  position: relative;
  height: 50rpx;
  line-height: 100rpx;
  overflow: hidden;
  background-color: rgba(182, 177, 157, 0.322);
}

/*评论滚动组件 swiper scroll*/
.msg-swiper-scroll {
  position: relative;
  height: 100%;
  width: 100%;
  line-height: 100rpx;
}

/*评论滚动组件 swipe item*/
.msg-swiper-scroll swiper-item {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

/*评论滚动组件 文字*/
.msg-text {
  color: rgb(255, 255, 255);
  position: relative;
}

/*评论滚动组件 头像*/
.scroll-avatar { 
  width: 30rpx;
  height: 30rpx;
  border-radius: 200rpx;
}

/*评论滚动组件 cover*/
.scroll-msg-cover {
  position: absolute;
  top: 0;
  z-index: 9999;
  height: 100%;
  width: 100%;
}

.background{
  position: absolute;
  z-index: -9999;
  height: 100%;
  width: 100%;
}

#blur{
  filter:blur(10px);
  -webkit-filter:blur(10px);
  -moz-filter:blur(10px);
  -ms-filter:blur(10px);
  -o-filter:blur(10px);
}

.bigPic{ 
  position: absolute;
  height:100%;
  width:100%;
  border-radius: 1.3%;
  box-shadow: 7.2464rpx 7.2464rpx 7.2464rpx 9.058rpx rgba(227, 200, 253, 0.384);
}
  
/*商铺组件的背景*/
#model {
  border-radius: 100%;
  position: absolute;
  width: 108.696rpx;
  height: 108.696rpx;
  margin-top: 875.0028rpx;
  margin-left: 50.9132rpx;
}

/*商铺组件*/
#modelImg {
  position: absolute;
  width: 126.812rpx;
  height: 126.812rpx;
  margin-top: 865.9448rpx;
  margin-left: 41.6668rpx;
}

/*点赞组件*/
#like {
  position: absolute;
  width: 77rpx;
  height: 77rpx;
  margin-top: 1098rpx;
  margin-left: 65rpx;
}

/*点赞组件*/
#share {
  position: absolute;
  width: 73rpx;
  height: 68rpx;
  margin-top: 1100rpx;
  margin-left: 200rpx;
}

/*点赞按钮（隐藏、按钮的穿透）*/
#share2 {
  position: absolute;
  width: 68rpx;
  height: 68rpx;
  border-radius: 30rpx;
  margin-top: 1110rpx;
  margin-left: 200rpx;
  color: rgb(255, 255, 255);
  font-size: 14px;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 25px;
  padding-right: 25px;
  background: rgba(230, 98, 98, 0);
}

/*点赞数*/
#num_like {
  position: absolute;
  width: 41.6668rpx;
  height: 36.232rpx;
  margin-top: 1170rpx;
  margin-left: 75rpx;
  font-size: 26rpx;
  color: whitesmoke;
  font-weight: 500;
}

/*分享数*/
#num_share {
  position: absolute;
  width: 41.6668rpx;
  height: 36.232rpx;
  margin-top: 1170rpx;
  margin-left: 213rpx;
  font-size: 26rpx;
  color: whitesmoke;
  font-weight: 500;
}
````

## index.js
````
//获取应用实例
var app = getApp()

Page({
  /**
   * 页面的初始数据
   */
  data: {
    screenHeight: app.screenHeight, //获取屏幕高度
    statusBarHeight: app.statusBarHeight, //获取状态栏高度
    navBarHeight: app.navBarHeight, //获取导航栏高度
    changeIndex: 0,
    // 显示或隐藏点赞与不点赞组件
    unlikeHidden: false,
    likeHidden: true,
    // 点赞次数
    likenum: 266,
    // 分享次数
    sharenum: 68,
    talks: [],
    teachFlag1: true,
    goodsPic: [{
      id: 0,
      url: "http://img5.imgtn.bdimg.com/it/u=3008581445,3045473788&fm=26&gp=0.jpg"
    }, {
      id: 1,
      url: "http://img1.imgtn.bdimg.com/it/u=272595693,824073970&fm=26&gp=0.jpg"
    }, {
      id: 2,
      url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1593412178846&di=bfc4741505ffe600565a6bf3394c791e&imgtype=0&src=http%3A%2F%2Fimg13.360buyimg.com%2Fn1%2Fs350x449_jfs%2Ft22660%2F67%2F1288630685%2F314518%2Fb8daa893%2F5b59f903N9e81f439.jpg%2521cc_350x449.jpg"
    }, {
      id: 3,
      url: "http://img0.imgtn.bdimg.com/it/u=3596338952,2751775316&fm=26&gp=0.jpg"
    }, {
      id: 4,
      url: "http://img1.imgtn.bdimg.com/it/u=272595693,824073970&fm=26&gp=0.jpg"
    }, {
      id: 5,
      url: "http://img5.imgtn.bdimg.com/it/u=3008581445,3045473788&fm=26&gp=0.jpg"
    }, {
      id: 6,
      url: "http://img1.imgtn.bdimg.com/it/u=272595693,824073970&fm=26&gp=0.jpg"
    }, {
      id: 7,
      url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1593412178846&di=bfc4741505ffe600565a6bf3394c791e&imgtype=0&src=http%3A%2F%2Fimg13.360buyimg.com%2Fn1%2Fs350x449_jfs%2Ft22660%2F67%2F1288630685%2F314518%2Fb8daa893%2F5b59f903N9e81f439.jpg%2521cc_350x449.jpg"
    }, {
      id: 8,
      url: "http://img0.imgtn.bdimg.com/it/u=3596338952,2751775316&fm=26&gp=0.jpg"
    }, {
      id: 9,
      url: "http://img1.imgtn.bdimg.com/it/u=272595693,824073970&fm=26&gp=0.jpg"
    }],
    scrollMsg: [{
      "avatar": "../../pic/home/avatar.png",
      "nickName": "云淡风轻",
      "content": "衬衫的手感真心不错哦！"
    }, {
      "avatar": "../../pic/home/avatar.png",
      "nickName": "拉普拉",
      "content": "22衬衫的手感真心不错哦！"
    }]
  },
  //划动切换
  slide(e) {
    var _ = e.detail.current
    var _t = this.data.tFlag
    // 用户完成用户教程之上下滑动
    if (_ == 3) {
      // 用户还没有完成所有教程
      if (!_t) {
        this.setData({
          changeIndex: _,
          teachFlag2: true,
          teachFlag1: false
        })
        this.teachToDt()
        return
      }
      // 用户完成所有教程
      this.setData({
        changeIndex: _
      })
      return
    }
    this.setData({
      changeIndex: _
    })
    console.log(_)
  },
  // 点赞
  like: function() {
    this.setData({
      unlikeHidden: true,
      likeHidden: false,
      likenum: this.data.likenum + 1
    })
    wx.showToast({
      title: '点赞成功',
      icon: 'success',
      duration: 1000
    })
  },
  // 取消点赞
  unlike: function() {
    this.setData({
      unlikeHidden: false,
      likeHidden: true,
      likenum: this.data.likenum - 1
    })
    wx.showToast({
      title: '取消点赞',
      icon: 'success',
      duration: 1000
    })
  },
  // 前往商店页
  toShop: function() {
    wx.navigateTo({
      url: '/pages/shop/shop',
    })
  },
  // 前往商品详情页
  toDetail: function() {
    var _t = this.data.tFlag
    var _t1 = this.data.teachFlag1
    if (_t || _t1 == false) {
      app.globalData.clickflag = true
      this.setData({
        tFlag: true,
        teachFlag1: true
      })
    }
    wx.navigateTo({
      url: '/pages/detail/detail'
    })
  },
  clikefromhere: function() {
    // 隐藏教程
    app.globalData.clickflag = true,
    this.setData({
      tFlag: true,
      teachFlag1: true
    })
    this.toDetail()
  },
  onLoad: function() {
    // 设置用户教程的布尔值
    var _tFlag = app.globalData.clickflag
    this.setData({
      tFlag: _tFlag
    })
    // 用户教程为false并且用户教程之点击详情页为false
    if (!_tFlag && this.data.teachFlag1) {
      var circleCount = 0;
      // 心跳的外框动画  
      this.animationMiddleHeaderItem = wx.createAnimation({
        duration: 800, // 以毫秒为单位  
        timingFunction: 'linear',
        delay: 70,
        transformOrigin: '50% 50%',
        success: function(res) {}
      });
      setInterval(function() {
        if (circleCount % 2 == 0) {
          this.animationMiddleHeaderItem.translateY(-100).step();
        } else {
          this.animationMiddleHeaderItem.translateY(0).step();
        }

        this.setData({
          animationMiddleHeaderItem: this.animationMiddleHeaderItem.export() //输出动画
        });

        circleCount++;
        if (circleCount == 1000) {
          circleCount = 0;
        }
      }.bind(this), 1000);
    }
  },
  teachToDt: function() {
    var circleCount = 0;
    // 心跳的外框动画  
    this.animationMiddleHeaderItem2 = wx.createAnimation({
      duration: 1000, // 以毫秒为单位  
      timingFunction: 'linear',
      delay: 100,
      transformOrigin: '50% 50%',
      success: function(res) {}
    });
    setInterval(function() {
      if (circleCount % 2 == 0) {
        this.animationMiddleHeaderItem2.scale(1.15).step();
      } else {
        this.animationMiddleHeaderItem2.scale(1.0).step();
      }

      this.setData({
        animationMiddleHeaderItem2: this.animationMiddleHeaderItem2.export() //输出动画
      });

      circleCount++;
      if (circleCount == 1000) {
        circleCount = 0;
      }
    }.bind(this), 1000);
  }
})
````
