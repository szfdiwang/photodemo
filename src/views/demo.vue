<template>
  <div class="img_container">
    <div class="btn_Bar">
      <button class="btn" @click="showType" :class="{'active':curstatus == 1}">分类</button>
      <button class="btn" @click="showTime" :class="{'active':curstatus == 2}">时间</button>
    </div>
    <div class="warp_box" @drop="drop" @dragover.prevent v-for="(item,index) in newImgList" ::key="index">
      <div v-if="curstatus==1" class="titile_box">{{item[0]['type']}}</div>
      <div :id="item[0].type" class="img_box">
        <div class="img_mini_box" draggable="true" @dragstart="dragstart($event,img)" @dragend="dragend"
          v-for="(img, index) in item" :key="img.id">
          <img :src="getUrl(img.url)" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {

    data() {
      return {
        curstatus: 1,
        toolList: [],
        armorList: [],
        holyList: [],
        wandList: [],
        weaponList: [],
        newImgList: [],
        imgList: [{
            id: 0,
            name: "穷鬼盾",
            type: "armor",
            createtime: "1101",
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
            createtime: "1103",
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
            createtime: "1210",
            url: "bottle"
          },
          {
            id: 10,
            name: "芒果",
            type: "tool",
            createtime: "1111",
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
            createtime: "1313",
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
            createtime: "915",
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
            createtime: "1317",
            url: "dark"
          },
          {
            id: 17,
            name: "圣剑",
            type: "weapon",
            createtime: "1218",
            url: "holy"
          },
          {
            id: 18,
            name: "狂战",
            type: "weapon",
            createtime: "119",
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
    directives: {
      drag: {
        bind: function (el) {
          console.log(el)
          let odiv = el; //获取当前元素
          odiv.onmousedown = (e) => {
            console.log(e)
            //算出鼠标相对元素的位置
            let disX = e.clientX - odiv.offsetLeft;
            let disY = e.clientY - odiv.offsetTop;

            document.onmousemove = (e) => {
              //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
              let left = e.clientX - disX;
              let top = e.clientY - disY;

              //绑定元素位置到positionX和positionY上面
              this.positionX = top;
              this.positionY = left;

              //移动当前元素
              odiv.style.left = left + 'px';
              odiv.style.top = top + 'px';
            };
            document.onmouseup = (e) => {
              document.onmousemove = null;
              document.onmouseup = null;
            };
          };
        }
      }
    },
    methods: {
      getIndex(arr, obj) {
        let len = arr.length;
        for (var i = 0; i < len; i++) {
          if (arr[i].id == obj.id) {
            return parseInt(i);
          }
        }
        return false;
      },
      arySplice(fromList, droppedImg) {
        fromList.splice(this.getIndex(fromList, droppedImg), 1)
      },
      drop(event) {
        console.log('drop', event)
        event.preventDefault()
        let fromList
        this.droppedImg = JSON.parse(event.dataTransfer.getData('img'))
        this.fromList = JSON.parse(event.dataTransfer.getData('fromList'))
        if (!!event.target.parentNode.parentNode.id) { //是否落在框中
          const tarDivId = event.target.parentNode.parentNode.id
          switch (tarDivId) {
            case "weapon":
              this.arySplice(this._data[`${this.fromList}List`], this.droppedImg)
              this.droppedImg.type = "weapon";
              this.weaponList.push(this.droppedImg);
              break;
            case "armor":
              this.arySplice(this._data[`${this.fromList}List`], this.droppedImg)
              this.droppedImg.type = "armor";
              this.armorList.push(this.droppedImg);
              break;
            case "holy":
              this.arySplice(this._data[`${this.fromList}List`], this.droppedImg)
              this.droppedImg.type = "holy";
              this.holyList.push(this.droppedImg);
              break;
            case "wand":
              this.arySplice(this._data[`${this.fromList}List`], this.droppedImg)
              this.droppedImg.type = "wand";
              this.wandList.push(this.droppedImg);
              break;
            case "tool":
              this.arySplice(this._data[`${this.fromList}List`], this.droppedImg)
              this.droppedImg.type = "tool";
              this.toolList.push(this.droppedImg);
              break;
            default:
              break;
          }
        } else {
          return false;
        }
      },
      dragstart(event, img) {
        console.log('dragstart', event)
        console.log('dragstart', img)
        event.dataTransfer.setData('img', JSON.stringify(img))
        event.dataTransfer.setData('fromList', JSON.stringify(img.type))
      },
      dragend(event) {
        console.log('dragend', event);
        event.dataTransfer.clearData()
      },
      clearList() {
        this.weaponList = [];
        this.holyList = [];
        this.wandList = [];
        this.toolList = [];
        this.armorList = [];
      },
      showType() {
        this.curstatus = 1
        this.clearList();
        this.imgList.map(item => {
          switch (item.type) {
            case "weapon":
              this.weaponList.push(item);
              break;
            case "armor":
              this.armorList.push(item);
              break;
            case "holy":
              this.holyList.push(item);
              break;
            case "wand":
              this.wandList.push(item);
              break;
            case "tool":
              this.toolList.push(item);
              break;
            default:
              break;
          }
        })
        this.newImgList = Object.assign({
          'weapon': this.weaponList
        }, {
          'armor': this.armorList
        }, {
          'holy': this.holyList
        }, {
          'wand': this.wandList
        }, {
          'tool': this.toolList
        })
      },
      sortFn(a, b) {
        return Number(a.createtime) - Number(b.createtime);
      },
      showTime() {
        this.curstatus = 2
        this.newImgList = []
        this.imgList.sort(this.sortFn)
        this.newImgList = Object.assign({
          'ByTime': this.imgList
        })
      },
      getUrl(url) {
        return require(`../assets/img/dota/${url}.png`)
      }
    },

    mounted() {
      this.showType();
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

    .btn_Bar {
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


    .warp_box {
      margin: 20px;

      .titile_box {
        width: 100px;
        text-align: center;
        font-size: 20px;
        font-weight: 400;
        color: #333333;
        background-color: #3CB371;
      }

      .img_box {
        display: flex;
        // margin-top: 20px;
        max-width: 600px;
        height: auto;
        flex-flow: row wrap;

        .img_mini_box {
          padding: 10px;
          background-color: #333333;
          cursor: pointer;

          img {
            width: 100px;
            height: 100px;
          }
        }
      }
    }

  }

</style>
