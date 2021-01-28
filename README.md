# 基于微信小程序Swiper组件实现精简交互技术实现

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
