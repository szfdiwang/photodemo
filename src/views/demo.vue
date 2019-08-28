<template>
  <div class="img_container">
    <div class="btnBar">
      <button class="btn" @click="showType" :class="{'active':curstatus == 1}">分类</button>
      <button class="btn" @click="showTime" :class="{'active':curstatus == 2}">时间</button>
    </div>
    <div class="img_warp">
      <div class="img_box" v-for="(img, index) in imgList" :key="img.id">
        <img :src="getUrl(img.url)" />
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        curstatus: 1,
        imgList: [{
            id: 0,
            name: "穷鬼盾",
            type: "armor",
            createtime: "1001",
            url: "poor"
          },
          {
            id: 1,
            name: "冰甲",
            type: "armor",
            createtime: "1002",
            url: "icearmor"
          },
          {
            id: 2,
            name: "强袭胸甲",
            type: "armor",
            createtime: "1003",
            url: "assault"
          },
          {
            id: 3,
            name: "赤红甲",
            type: "armor",
            createtime: "1004",
            url: "red"
          },
          {
            id: 4,
            name: "龙心",
            type: "holy",
            createtime: "1005",
            url: "dragon"
          },
          {
            id: 5,
            name: "冰眼",
            type: "holy",
            createtime: "1006",
            url: "iceeye"
          },
          {
            id: 6,
            name: "玲珑心",
            type: "holy",
            createtime: "1007",
            url: "linglong"
          },
          {
            id: 7,
            name: "补刀斧",
            type: "tool",
            createtime: "1008",
            url: "blade"
          },
          {
            id: 8,
            name: "小蓝",
            type: "tool",
            createtime: "1009",
            url: "blue"
          },
          {
            id: 9,
            name: "瓶子",
            type: "tool",
            createtime: "1010",
            url: "bottle"
          },
          {
            id: 10,
            name: "芒果",
            type: "tool",
            createtime: "1011",
            url: "mango"
          },
          {
            id: 11,
            name: "A杖",
            type: "wand",
            createtime: "1012",
            url: "ahalimu"
          },
          {
            id: 12,
            name: "黑皇杖",
            type: "wand",
            createtime: "1013",
            url: "bkb"
          },
          {
            id: 13,
            name: "羊刀",
            type: "wand",
            createtime: "1014",
            url: "sheep"
          },
          {
            id: 14,
            name: "风杖",
            type: "wand",
            createtime: "1015",
            url: "wind"
          },
          {
            id: 15,
            name: "大炮",
            type: "weapon",
            createtime: "1016",
            url: "cannon"
          },
          {
            id: 16,
            name: "暗灭",
            type: "weapon",
            createtime: "1017",
            url: "dark"
          },
          {
            id: 17,
            name: "圣剑",
            type: "weapon",
            createtime: "1018",
            url: "holy"
          },
          {
            id: 18,
            name: "狂战",
            type: "weapon",
            createtime: "1019",
            url: "mad"
          },
          {
            id: 19,
            name: "雷神之锤",
            type: "weapon",
            createtime: "1020",
            url: "quake"
          },
        ]
      }
    },
    methods: {
      showType() {
        this.curstatus = 1
      },
      showTime() {
        this.curstatus = 2
      },
      getUrl(url) {
        return require(`../assets/img/dota/${url}.png`)
      }
    },

    mounted() {

    },
  }

</script>
<style lang="scss">
  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    padding: 0;
  }

  .img_container {
    padding: 20px;

    .btnBar {
      .active {
        background-color: #426fc5;
        color: #fff;
      }

      button {
        cursor: pointer;
      }

      button:not(:first-child) {
        margin-left: 10px;
      }

    }

    .img_warp {
      display: flex;
      border: 1px solid #d9d9d9;
      margin-top: 20px;

      .img_box {
        padding: 10px;

        img {
          width: 100px;
          height: 100px;
        }
      }
    }
  }

</style>
