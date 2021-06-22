<template>
  <view class="content">
    <!-- 头部区域开始 -->
    <view class="header">
      <view class="leftIcon">
        <image src="../../static/img/1.png" mode="" />
      </view>
      <view class="right">
        <view class="topBox">
          <text>青团保障</text><text>|</text><text>兼职无忧</text>
        </view>
        <view class="bottomBox"> 11重岗位审核1000万薪资保障100%客服响应 </view>
      </view>
    </view>
    <!-- 头部区域结束 -->
    <!-- 搜索开始 -->
    <view class="search">
      <view class="address"
        ><text class="icon-icon-test iconfont"></text>
        <text class="text">贵阳</text>
      </view>
      <!-- 搜索条 -->
      <view class="searchBox">
        <text class="iconfont .icon-search"></text>
        <text class="text1">{{ texts }}</text>
      </view>
      <!-- 签到 -->
      <view class="qiandao">
        <navigator url="#" redirect hover-class="className">
          <image src="../../static/img/2.png" mode="aspectFit" />
        </navigator>
      </view>
    </view>
    <!-- 搜索结束 -->
    <!-- 选项卡开始 -->
    <view class="seceltCard">
      <view class="card">
        <view class="img"><image src="../../static/img/3.png" mode="" /></view>
        <view class="text2">宅家赚钱</view>
      </view>
      <view class="card">
        <view class="img"><image src="../../static/img/3.png" mode="" /></view>
        <view class="text2">高薪兼职</view>
      </view>
      <view class="card">
        <view class="img"><image src="../../static/img/3.png" mode="" /></view>
        <view class="text2">答题赚青豆</view>
      </view>
      <view class="card">
        <view class="img"><image src="../../static/img/3.png" mode="" /></view>
        <view class="text2">极速上岗</view>
      </view>
      <view class="card">
        <view class="img"><image src="../../static/img/3.png" mode="" /></view>
        <view class="text2">课程培训</view>
      </view>
    </view>
    <!-- 选项卡结束 -->
    <!-- 轮播图开始 -->

    <view class="scroll1">
      <scroll-view scroll-x="true" class="scrollx">
        <view class="scroll">
          <image src="../../static/img/4.png" mode="" />
          <image src="../../static/img/4.png" mode="" />
          <image src="../../static/img/4.png" mode="" />
        </view>
      </scroll-view>
    </view>

    <!-- 轮播图结束 -->
    <!-- 团子精选开始 -->
    <view class="selects">
      <image src="../../static/img/5.png" mode="" />
    </view>
    <!-- 团子精选结束 -->
    <!-- 推荐开始 -->
    <u-sticky class="recommend">
      <!-- <scroll-view scroll-x class="textScroll">
        <view class="scrollxx">
          <navigator
            v-for="(i, index) in recommend"
            :key="index"
            url="#"
            redirect
            hover-class="className"
            @tap="recommendClick(index)"
            :class="{ active: activeNum === index ? true : false }"
            >{{ i }}</navigator
          >
        </view>
      </scroll-view> -->
      <u-tabs
        name="cate_name"
        count="cate_count"
        :list="recommend"
        :is-scroll="true"
        class="uTabs"
        font-size="24rpx"
        @change="tabchange"
        :current="currenttab"
        active-color="black"
      ></u-tabs>
      <view class="btn">
        <u-button plain size="mini" class="btn1" @click="showWorkClick"
          >岗位类型</u-button
        >
        <u-button plain size="mini" @click="sortClick">默认排序</u-button>
        <u-button plain size="mini" class="btn3" @click="btn3Tap"
          >筛选</u-button
        >
      </view>
    </u-sticky>
    <!-- 推荐结束 -->
    <!-- 点击筛选的弹出层开始 -->
    <view class="getChose">
      <u-popup
        v-model="showChose"
        mode="bottom"
        border-radius="14"
        length="85%"
      >
        <view class="head">
          <view class="headtitle">筛选</view>
          <view class="headCancel" @click="cancelClick">取消</view>
        </view>
        <!-- 工作区域
         -->
        <view class="workarea">
          <view class="workareaTitle"> 工作区域 </view>
          <view class="area">
            <u-tag
              :text="i"
              mode="dark"
              v-for="(i, index) in areaWork"
              :bg-color="activeNum == index ? activeColor : activeColor1"
              :key="index"
              size="40rpx"
              @click="tagclick1(index)"
            />
          </view>
        </view>
        <!-- 工作区域 结束-->
        <!-- 结算方式 -->
        <view class="workareaTitle"> 结算方式 </view>
        <view class="area">
          <u-tag
            :text="i"
            mode="dark"
            v-for="(i, index) in pay"
            :bg-color="activeNum1 == index ? activeColor : activeColor1"
            :key="index"
            size="40rpx"
            @click="tagclick2(index)"
          />
        </view>
        <!-- 结算方式结束 -->
        <!-- x性别要求 -->
        <view class="workareaTitle"> 性别要求 </view>

        <view class="area">
          <u-tag
            :text="i"
            mode="dark"
            v-for="(i, index) in sex"
            :bg-color="activeNum3 == index ? activeColor : activeColor1"
            :key="index"
            size="40rpx"
            @click="tagclick3(index)"
          />
        </view>
        <!-- x性别要求结束 -->
        <view class="tagbtn">
          <u-button size="medium" class="reset" @click="resetClick"
            >重置</u-button
          >
          <u-button size="medium" type="success" class="sure" @click="sureClick"
            >确定</u-button
          >
        </view>
      </u-popup>
    </view>
    <!-- 点击筛选的弹出层结束 -->
    <!-- 岗位类型 -->
    <view class="works">
      <u-popup v-model="showWork" mode="bottom" border-radius="14" length="80%">
        <view class="head">
          <view class="headtitle">选择兼职类型</view>
          <view class="headCancel" @click="cancel1Click">取消</view>
        </view>
        <!-- 全部类型 -->
        <view class="scrollwork">
          <scroll-view
            scroll-y="true"
            class="workScroll"
            show-scrollbar="false"
          >
            <view class="scrolly">
              <view
                v-for="(i, index) in workss"
                :key="index"
                class="scrolly-item"
                @click="worksClick(index)"
                :class="{ activeWork: activeWork === index ? true : false }"
                >{{ i }}</view
              >
            </view>
          </scroll-view>
          <!-- 全部 -->
          <view
            class="all"
            v-for="(i, index) in workss"
            :key="index"
            v-show="index == activeWork ? true : false"
          >
            <view>{{ i }}</view>
            <view>{{ i + 1 }}</view>
            <view>{{ I + 2 }}</view>
          </view>
          <!-- 全部结束 -->
        </view>

        <!-- 全部类型结束 -->
      </u-popup>
    </view>
    <!-- 排序筛选开始 -->
    <view class="sort">
      <u-popup v-model="showSort" mode="bottom" border-radius="14" length="50%">
        <view class="head">
          <view class="headtitle">排序筛选</view>
          <view class="headCancel" @click="cancel2Click">取消</view>
        </view>
        <!-- 排序方式开始 -->
        <view class="sorts">
          <view
            v-for="(i, index) in sorts"
            :key="index"
            class="sortss"
            @click="sortsClick(index)"
            :class="{ sortActive: index === sortNum ? true : false }"
            >{{ i }}
          </view>
        </view>
        <!-- 排序方式结束 -->
      </u-popup>
    </view>

    <!-- 排序筛选结束 -->
    <!-- 底部选项卡片开始 -->
    <view
      class="footer"
      v-for="(i, inde) in 10"
      :key="inde"
      v-show="inde == currenttab ? true : false"
    >
      <view class="foot-item" v-for="(i, index) in 10" :key="index">
        <view class="footLeft">
          <view class="work">第{{ inde + 1 }}招聘美工设计兼职</view>
          <view class="business">杭州君弘科技有限公司</view>
        </view>
        <view class="footRight"> 388元/其他 </view>
      </view>
      <view class="refresh">
        <view class="refreshBtn" @click="showToast">
          <u-icon name="reload" color="#2979ff" size="32 "></u-icon>
          点击刷新更多优质岗位
        </view>
      </view>
      <view class="foot-item" v-for="(i, index) in 10" :key="index">
        <view class="footLeft">
          <view class="work">第{{ inde }}招聘美工设计兼职</view>
          <view class="business">杭州君弘科技有限公司</view>
        </view>
        <view class="footRight"> 388元/其他 </view>
      </view>
    </view>
    <!-- 底部选项卡片结束 -->
    <!-- toast开始 -->
    <view>
      <u-toast ref="uToast" />
    </view>
    <!-- toast结束 -->
  </view>
</template>

<script>
import uPopup from "../../uview-ui/components/u-popup/u-popup.vue";
export default {
  components: { uPopup },
  data() {
    return {
      // title: "Hello",
      textList: ["包吃住", "奶茶店", "保安", "服务员"],
      texts: "热点",
      recommend: [
        {
          cate_name: "推荐",
        },
        {
          cate_name: "在家做",
        },
        {
          cate_name: "在本地",
        },
        {
          cate_name: "主播",
        },
        {
          cate_name: "文案编辑",
        },
        {
          cate_name: "服务员",
        },
        {
          cate_name: "导购",
        },
        {
          cate_name: "在家培训",
        },
        {
          cate_name: "全职",
        },
        {
          cate_name: "实习",
        },
      ],
      // 控制推荐活跃
      isActive: false,

      // 点击筛选的显示隐藏
      showChose: false,
      // 选中的tab
      currenttab: 0,
      areaWork: [
        "不限",
        "南明区",
        "云岩区",
        "花溪区",
        "乌当区",
        "白云区",
        "开阳县",
        "息烽县",
        "修文县",
        "清镇市",
        "观山湖区",
      ],
      // 结算方式
      pay: ["不限", "日结", "周结", "月结", "完工结算", "其他结算"],
      sex: ["不限", "男生可做", "女生可做"],
      // 工作区活跃的下标
      activeNum: 0,
      // 结算下表
      activeNum1: 0,
      // 性别要求下标
      activeNum3: 0,
      // 工作活跃的北京
      activeColor: "#01ce8d",
      activeColor1: "#ccc",
      // 岗位类型弹出
      showWork: false,
      // 岗位
      workss: [
        "全部类型",
        "餐饮服务",
        "超市零售",
        "物流仓储",
        "市场推广",
        "家教培训",
        "展会演出",
        "线上兼职",
        "才艺技能",
        "客服话务",
        "文员助理",
        "线下主播",
        "其它",
      ],
      // 点击全部类型中的岗位活跃
      activeWork: 0,
      activeWorks: "activeWork",
      // 排序筛选显示
      showSort: false,
      sorts: ["默认排序", "离我最近", "最新发布", "热门岗位", "薪资最高"],
      sortNum: 0,
    };
  },
  computed: {
    bacolor() {
      return;
    },
  },
  onLoad() {
    this.changeSerach();
  },
  methods: {
    //改变搜索框中的字
    changeSerach() {
      var num = 0;
      setInterval(() => {
        // console.log(1);
        this.texts = this.textList[num];
        num++;
        if (num > 3) {
          num = 0;
        }
      }, 1000);
    },
    // scrolly-item
    // 点击推荐的
    recommendClick(e) {
      // console.log(e);
      this.activeNum = e;
    },
    // 点击筛选按钮
    btn3Tap() {
      // console.log(1);
      this.showChose = true;
    },
    // 取消筛选按钮
    cancelClick() {
      this.showChose = false;
    },
    // 点击tabs
    tabchange(index) {
      console.log(index);
      this.currenttab = index;
    },
    // 点击工作区域的tag
    tagclick1(e) {
      // console.log(e);
      this.activeNum = e;
    },
    //点击结算
    tagclick2(e) {
      // console.log(e);
      this.activeNum1 = e;
    },
    //性别要求

    tagclick3(e) {
      // console.log(e);
      this.activeNum3 = e;
    },
    // 筛选重置
    resetClick() {
      this.activeNum = 0;
      this.activeNum1 = 0;
      this.activeNum3 = 0;
    },
    //筛选确定
    sureClick() {
      this.showChose = false;
    },
    // 岗位类型的弹出
    showWorkClick() {
      this.showWork = true;
    },
    // 岗位类型的取消
    cancel1Click() {
      this.showWork = false;
    },
    // 点击全部类型中的岗位
    worksClick(e) {
      console.log(e);
      this.activeWork = e;
    },
    // 控制排序筛选弹出层
    sortClick() {
      this.showSort = true;
    },
    // 取消排序筛选
    cancel2Click() {
      this.showSort = false;
    },
    // 点击排序项目
    sortsClick(e) {
      this.sortNum = e;
    },
    showToast() {
      // console.log(22);
      this.$refs.uToast.show({
        title: "刷新成功",
        type: "success",
      });
    },
  },
};
</script>

<style>
/* 活跃的样式 */
.active {
  /* color: yellow; */
  font-size: 28rpx;
  display: inline-block;
  border-bottom: 3px solid green;
  /* border-radius: 20rpx; */
  /* position: absolute; */
  /* left: 0; */
}
.activeWork {
  color: green;
}
/* 排序活跃的样式 */
.sortActive {
  color: green;
}

.header {
  display: flex;
  height: 75rpx;
  width: 100vw;
  align-items: center;
}
.header .leftIcon {
  /* display: flex; */
  /* align-items: center; */
  padding-top: 16rpx;
  padding-left: 16rpx;
}
.header .right {
  margin-left: 10rpx;
}
.leftIcon image {
  width: 75rpx;
  height: 65rpx;
}
.header .bottomBox {
  font-size: 14rpx;
  color: #9e9fa3;
  /* transform: translate(0.3); */
}
.header .topBox text {
  font-size: 26rpx;
  font-weight: 700;
}
.header .topBox text:nth-child(2) {
  margin: 0 10rpx;
}
/* 搜索 */
.search {
  display: flex;
  margin: 16rpx 30rpx;
  height: 60rpx;
}
.search .address {
  flex: 4;
  display: flex;
  align-items: center;
}
.search .iconfont {
  font-size: 30rpx;
}
.search .address .text {
  font-size: 28rpx;
  margin-left: 10rpx;
  font-weight: 550;
}
.search .searchBox {
  flex: 12;
  background-color: #eee;
  border-radius: 25rpx;
  display: flex;
  align-items: center;
  height: 60rpx;
  color: #898999;
}
.search .searchBox .icon-search {
  font-size: 24rpx;
  margin-left: 30rpx;
  margin-right: 20rpx;
}
.search .searchBox .text1 {
  font-size: 20rpx;
}

.search .qiandao {
  flex: 3;
}
.search .qiandao image {
  width: 100%;
  /* height: 100%; */
  height: 60rpx;
}
/* 选项卡 */
.seceltCard {
  display: flex;
}
.seceltCard .card {
  flex: 1;
  width: 25%;
  margin: 10rpx;
  font-size: 18rpx;
  text-align: center;
}
.seceltCard .card image {
  width: 80%;
  /* height: 100%; */
  height: 80rpx;
}
/* 轮播图 */

.scrollx {
  /* 滚动视口的高度 */
  width: 100vw;
  height: 220rpx;
  display: flex;
  flex-wrap: nowrap;
}
.scroll1 {
  margin: 40rpx 0;
}
.scroll {
  /* 可滚动的距离 */
  width: 1725rpx;
}
.scrollx image {
  margin-left: 30rpx;
  width: 525rpx;
  height: 225rpx;
}
/* 团子精选 */
.selects {
  width: 210rpx;
  height: 90rpx;
}
.selects image {
  width: 100%;
  height: 100%;
}
/* 推荐 */
.textScroll {
  /* display: flex; */
  width: 750rpx;
  height: 66rpx;
}
.scrollxx {
  width: 1300rpx;
  /* width: 24rpx; */
  font-size: 24rpx;
  /* height: 100rpx; */
  display: flex;
}
.scrollxx navigator {
  margin: 0 30rpx;
  height: 55rpx;
}
.uTabs {
  font-size: 24rpx;
  color: red;
}
.btn3 {
  float: right;
  margin-right: 20rpx;
}
.btn1 {
  margin: 0 15rpx;
}
/* 帅选 */
.getChose .head {
  height: 100rpx;
  display: flex;
  /* justify-content: center; */
}
.getChose .head .headtitle {
  /* text-align: center; */
  /* line-height: 55rpx; */
  /* display: inline-block; */
  flex: 7;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 600;
}
.works .head {
  height: 100rpx;
  display: flex;
}
.sort .head {
  height: 100rpx;
  display: flex;
}
.head .headtitle {
  flex: 7;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 600;
}
.getChose .head .headCancel {
  /* float: right; */
  /* display: inline-block; */
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18rpx;
  color: #9e9fa3;
}
.head .headCancel {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18rpx;
  color: #9e9fa3;
}
/* tag标签 */
.u-tag {
  width: 220rpx;
  height: 50rpx;
  margin: 20rpx 0rpx 0 20rpx;

  text-align: center;
  line-height: 50rpx !important;
  /* vertical-align: center; */
}
/* 筛选的重置和确定按钮 */
.tagbtn {
  /* display: flex; */
  margin: 60rpx 20rpx;
}
.tagbtn .sure {
  float: right;
}

.tagbtn .reset {
  /* flex: 3; */
  width: 225rpx !important;
}
/* title筛选 */
.workareaTitle {
  margin: 15rpx 20rpx;
}
.workareaTitle:nth-child(1) {
  margin: 0 20rpx;
}
/* 全部类型 岗位类型
 */
.workScroll {
  height: 700rpx;
}
.scrolly {
  height: 820rpx;
}
.scrolly .scrolly-item {
  margin: 35rpx 30rpx;
}
.scrollwork {
  display: flex;
}
.scrollwork .workScroll {
  flex: 3;
}
::webkit-scrollbar {
  width: 0;
}

.scrollwork .all {
  flex: 8;
  background-color: #ccc;
  border-radius: 25rpx;
  margin-right: 20rpx;
  padding: 25rpx;
}
.scrollwork .all view {
  margin: 15rpx;
}
.sorts {
  display: flex;
  flex-direction: column;
}
.sorts .sortss {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 25rpx 0;
  font-size: 22rpx;
}
.foot-item {
  display: flex;
  padding: 20rpx;
  background-color: #ffffff;
  margin: 20rpx 20rpx;
  border-radius: 15rpx;
}
.foot-item .footLeft {
  flex: 7;
  font-size: 22rpx;
}
.foot-item .footLeft .business {
  color: #a3a3a3;
  font-size: 18rpx;
}
.foot-item .footRight {
  flex: 3;
  color: #e56873;
}
.content {
  background-color: #f4f3f8;
}
.recommend {
  background-color: #ffffff;
}
.btn {
  background-color: #ffffff;
  padding-bottom: 20rpx;
}
.refreshBtn {
  width: 375rpx;
  height: 90rpx;
  margin: 30rpx 175rpx;
  background-color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 30rpx;
}
.refreshBtn .u-icon {
  background-color: #1aa034;
  border-radius: 50%;
  color: black;
}
.btn {
  margin-right: 30rpx;
}
/* 隐藏滚动条 */
::-webkit-scrollbar {
  width: 0;
  height: 0;
  background-color: transparent;
}
</style>
