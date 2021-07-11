<template>
  <div id="lucky-bag">
    <div class="section-title">
      <div class="title-decor">
        <span class="dot"></span>
        <span class="dot"></span>
        <span class="dot"></span>
      </div>
      <div class="title-content-container">
        <div class="title-content">
          <p>新年期間限定福袋，限量組合要搶要快！</p>
        </div>
      </div>
    </div>
    <div class="lesson-list">
      <div v-for="(list, title) in lessonList" :key="list" class="col">
        <div class="decor" :class="title">
          <div class="triangle"></div>
          <div class="line-group">
            <div class="line"></div>
            <div class="line"></div>
            <div class="line"></div>
          </div>
          <div class="square-group">
            <div class="square"></div>
            <div class="square"></div>
          </div>
          <div v-if="devicePath === 'desktop'" class="triangle"></div>
        </div>
        <div class="main-title">
          <img src="@/assets/reel.png" alt="title" />
          <span>{{ nameMapping[title] }}</span>
        </div>
        <div
          v-for="lesson in list"
          :key="lesson"
          class="bag"
          :class="{
            selected: getSelected(title, lesson),
          }"
        >
          <img src="@/assets/handler.png" class="handler" alt="handler" />
          <img
            :src="require(`@/assets/lesson-${lesson.imgId}.png`)"
            alt="lesson"
          />
          <p class="title">{{ lesson.title }}</p>
          <div class="info">
            <div class="number-info">
              <div class="teacher">
                <img
                  :src="require(`@/assets/teacher-${lesson.teacher.id}.png`)"
                  :alt="`${lesson.teacher.name}`"
                />
                <span>{{ lesson.teacher.name }}</span>
              </div>
              <span class="price-sale">${{ lesson.price.sale }}</span>
              <span class="price-original">${{ lesson.price.original }}</span>
            </div>
            <div class="limit">限量<br />{{ lesson.limit }}位</div>
          </div>
        </div>
        <button
          v-if="devicePath !== 'desktop'"
          class="arrow arrow-left"
          :disabled="checkDisabled(title, 'left')"
          @click="slide(title, 'left')"
        >
          <img src="@/assets/arrow-left.png" alt="arrow-left" />
        </button>
        <button
          v-if="devicePath !== 'desktop'"
          class="arrow arrow-right"
          :disabled="checkDisabled(title, 'right')"
          @click="slide(title, 'right')"
        >
          <img src="@/assets/arrow-right.png" alt="arrow-right" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, inject } from 'vue';

export default defineComponent({
  name: 'LuckyBag',
  setup() {
    const devicePath = inject('devicePath');

    return {
      devicePath,
    };
  },
  data() {
    return {
      lessonList: {
        frontEnd: [
          {
            id: 1,
            title: '互動式網頁動畫完全手冊',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 19399,
              sale: 7090,
            },
            limit: 5,
            imgId: 1,
          },
          {
            id: 2,
            title: '2020 Vue 3 專業職人完成組合 | 入門篇＋進階篇＋加值篇',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 9600,
              sale: 3300,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 3,
            title: '雙系列組合 | JavaScript + Vue 3前導專業職人之路',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 25799,
              sale: 7690,
            },
            limit: 15,
            imgId: 3,
          },
        ],
        backEnd: [
          {
            id: 4,
            title: 'PHP+Laravel 8完整建構電商攻略',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8500,
              sale: 3490,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 5,
            title: 'Django+Flask雙組合｜從0到1快速打造直播聊天網站',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 15,
            imgId: 3,
          },
        ],
        common: [
          {
            id: 6,
            title: '從LeetCode學演算法｜完整解題技巧＋面試成功指南',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8500,
              sale: 3490,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 7,
            title: 'API整合實戰系列課程',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 15,
            imgId: 3,
          },
          {
            id: 8,
            title: '工程師學接案｜JaveScript基礎養成包',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 5,
            imgId: 3,
          },
        ],
        trading: [
          {
            id: 9,
            title: '從LeetCode學演算法｜完整解題技巧＋面試成功指南',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8500,
              sale: 3490,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 10,
            title: 'API整合實戰系列課程',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 15,
            imgId: 3,
          },
          {
            id: 11,
            title: '工程師學接案｜JaveScript基礎養成包',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 5,
            imgId: 3,
          },
        ],
        AI: [
          {
            id: 12,
            title: '從LeetCode學演算法｜完整解題技巧＋面試成功指南',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8500,
              sale: 3490,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 13,
            title: 'API整合實戰系列課程',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 15,
            imgId: 3,
          },
        ],
        devOp: [
          {
            id: 14,
            title: '從LeetCode學演算法｜完整解題技巧＋面試成功指南',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8500,
              sale: 3490,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 15,
            title: 'API整合實戰系列課程',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 15,
            imgId: 3,
          },
          {
            id: 16,
            title: '工程師學接案｜JaveScript基礎養成包',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 5,
            imgId: 3,
          },
        ],
        app: [
          {
            id: 17,
            title: '從LeetCode學演算法｜完整解題技巧＋面試成功指南',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8500,
              sale: 3490,
            },
            limit: 15,
            imgId: 2,
          },
          {
            id: 18,
            title: 'API整合實戰系列課程',
            teacher: {
              id: 622,
              name: 'Mike',
            },
            price: {
              original: 8600,
              sale: 3790,
            },
            limit: 15,
            imgId: 3,
          },
        ],
      },
      selectedItemList: {
        frontEnd: 1,
        backEnd: 4,
        common: 6,
        trading: 9,
        AI: 12,
        devOp: 14,
        app: 17,
      },
      nameMapping: {
        frontEnd: '前端',
        backEnd: '後端',
        common: '通用',
        trading: '程式交易',
        AI: '人工智慧',
        devOp: '維運',
        app: '手機',
      },
    };
  },
  methods: {
    getSelected(title, lesson) {
      if (lesson.id === this.selectedItemList[title]) {
        return true;
      }
      return false;
    },
    slide(title, type) {
      const index = this.lessonList[title].findIndex(
        (item) => item.id === this.selectedItemList[title],
      );
      let newIndex;
      if (type === 'left') {
        newIndex = index - 1 >= 0 ? index - 1 : index;
      } else {
        newIndex = index + 1 < this.lessonList[title].length ? index + 1 : index;
      }
      this.selectedItemList[title] = this.lessonList[title][newIndex].id;
    },
    checkDisabled(title, type) {
      const index = this.lessonList[title].findIndex(
        (item) => item.id === this.selectedItemList[title],
      );
      if (type === 'left' && index === 0) {
        return true;
      }
      if (type === 'right' && index === this.lessonList[title].length - 1) {
        return true;
      }
      return false;
    },
  },
});
</script>

<style lang="scss" scoped>
@import "@/styles/variables.scss";

#lucky-bag {
  @include rwdmax($tablet - 1) {
    margin-top: 70px;
  }
  @include rwd($tablet, $desktop - 1) {
    margin-top: 70px;
  }
  @include rwdmin($desktop) {
    margin-top: 70px;
  }
  .section-title {
    p {
      margin: 0;
    }
  }
  .lesson-list {
    @include rwdmax($tablet - 1) {
      margin-top: 70px;
    }
    @include rwd($tablet, $desktop - 1) {
      margin-top: 70px;
    }
    @include rwdmin($desktop) {
      margin-top: 70px;
    }
  }
  .col {
    background-color: $gray;
    position: relative;
    display: flex;
    @include rwdmax($tablet - 1) {
      padding: 18% 18% 32px;
      &:not(:last-child) {
        margin-bottom: 70px;
      }
    }
    @include rwd($tablet, $desktop - 1) {
      padding: 15% 25% 32px;
      &:not(:last-child) {
        margin-bottom: 70px;
      }
    }
    @include rwdmin($desktop) {
      width: 75%;
      margin: auto;
      justify-content: center;
      padding: 76px 50px 40px;
      &:not(:last-child) {
        margin-bottom: 170px;
      }
    }
    .main-title {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      @include rwdmax($tablet - 1) {
        width: 40%;
      }
      @include rwd($tablet, $desktop - 1) {
        width: 32%;
      }
      @include rwdmin($desktop) {
        width: 20%;
      }
      img {
        width: 100%;
      }
      span {
        color: $gray;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -60%);
        @include rwdmax($tablet - 1) {
          font-size: 18px;
        }
        @include rwdmin($tablet) {
          font-size: 26px;
        }
      }
    }
    .bag {
      width: 100%;
      display: flex;
      flex-wrap: wrap;
      padding: 10px;
      background: $beige;
      position: relative;
      @include rwdmax($desktop - 1) {
        margin-right: -100%;
        visibility: hidden;
        backface-visibility: hidden;
        border: 1px solid $brown;
      }
      @include rwdmin($desktop) {
        width: 24%;
        margin: 20px;
        border: 1px solid $brown;
      }
      &.selected {
        visibility: visible;
        box-shadow: 5px 5px $deep-brown;
      }
      .handler {
        display: block;
        content: "";
        width: 60%;
        position: absolute;
        top: 0;
        left: 20%;
        transform: translateY(-100%);
      }
      img {
        width: 100%;
      }
      .title {
        color: $deep-brown;
        font-weight: bold;
        @include rwdmax($tablet - 1) {
          font-size: 18px;
        }
        @include rwd($tablet, $desktop - 1) {
          font-size: 26px;
        }
        @include rwdmin($desktop) {
          font-size: 18px;
        }
      }
      .info {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
      }
      .number-info {
        width: 65%;
        .teacher {
          color: $deep-brown;
          img {
            @include rwdmax($tablet - 1) {
              width: 30px;
              margin-right: 5px;
            }
            @include rwd($tablet, $desktop - 1) {
              width: 30px;
              margin-right: 10px;
            }
            @include rwdmin($desktop) {
              width: 30px;
              margin-right: 15px;
            }
          }
          span {
            @include rwdmax($tablet - 1) {
              font-size: 16px;
            }
            @include rwd($tablet, $desktop - 1) {
              font-size: 18px;
            }
            @include rwdmin($desktop) {
              font-size: 28px;
            }
          }
          img,
          span {
            vertical-align: middle;
          }
        }
        .price-sale {
          color: #ba3f2f;
          @include rwdmax($tablet - 1) {
            font-size: 26px;
            margin-right: 5px;
          }
          @include rwd($tablet, $desktop - 1) {
            font-size: 26px;
            margin-right: 10px;
          }
          @include rwdmin($desktop) {
            font-size: 26px;
            margin-right: 15px;
          }
        }
        .price-original {
          color: $deep-brown;
          text-decoration: line-through;
          @include rwdmax($tablet - 1) {
            font-size: 16px;
          }
          @include rwd($tablet, $desktop - 1) {
            font-size: 18px;
          }
          @include rwdmin($desktop) {
            font-size: 16px;
          }
        }
      }
      .limit {
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        width: 70px;
        height: 70px;
        border-radius: 50%;
        background: $yellow;
        border: 1.5px solid #be9360;
        color: $deep-brown;
        position: relative;
        @include rwdmax($tablet - 1) {
          font-size: 16px;
        }
        @include rwd($tablet, $desktop - 1) {
          font-size: 18px;
        }
        @include rwdmin($desktop) {
          font-size: 18px;
        }
        &:before {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          border-radius: 50%;
          content: "";
          display: block;
          width: 54px;
          height: 54px;
          border: 1.5px solid #be9360;
        }
      }
    }
    .arrow {
      position: absolute;
      top: 49%;
      background: none;
      border: none;
      padding: 0;
      @include rwdmax($tablet - 1) {
        width: 40px;
      }
      @include rwd($tablet, $desktop - 1) {
        width: 46px;
      }
      @include rwdmin($desktop) {
        width: 90px;
      }
      img {
        width: 100%;
      }
      &.arrow-left {
        left: 20px;
      }
      &.arrow-right {
        right: 20px;
      }
      &:disabled {
        opacity: 0.5;
      }
    }
    .decor {
      position: absolute;
      top: 8px;
      bottom: 8px;
      left: 8px;
      right: 8px;
      content: "";
      display: block;
      border: 2px solid $brown;
      background-size: 100%;
      background-position: top;
      background-repeat: no-repeat;
      @include rwdmin($desktop) {
        &.frontEnd {
          background-image: url("~@/assets/desktop/logo-backgound-frontEnd.png");
        }
        &.backEnd {
          background-image: url("~@/assets/desktop/logo-backgound-backEnd.png");
        }
        &.common {
          background-image: url("~@/assets/desktop/logo-backgound-common.png");
        }
        &.trading {
          background-image: url("~@/assets/desktop/logo-backgound-trading.png");
        }
        &.AI {
          background-image: url("~@/assets/desktop/logo-backgound-AI.png");
        }
        &.devOp {
          background-image: url("~@/assets/desktop/logo-backgound-devOp.png");
        }
        &.app {
          background-image: url("~@/assets/desktop/logo-backgound-app.png");
        }
      }
      .triangle {
        width: 0;
        height: 0;
        border-style: solid;
        border-width: 0 34px 34px 0;
        border-color: transparent $orange transparent transparent;
        position: absolute;
        top: 0;
        right: 0;
        @include rwdmax($tablet - 1) {
          border-width: 0 34px 34px 0;
        }
        @include rwd($tablet, $desktop - 1) {
          border-width: 0 50px 50px 0;
        }
        @include rwdmin($desktop) {
          border-width: 0 56px 56px 0;
        }
        &:last-child {
          border-width: 56px 0 0 56px;
          border-color: transparent transparent transparent $orange;
          bottom: 0;
          left: 0;
          top: unset;
          right: unset;
        }
      }
      .line-group {
        position: absolute;
        top: 30px;
        left: -8px;
        .line {
          background-color: #590a10;
          margin-bottom: 3px;
          @include rwdmax($tablet - 1) {
            width: 34px;
            height: 6px;
          }
          @include rwd($tablet, $desktop - 1) {
            width: 95px;
            height: 8px;
          }
          @include rwdmin($desktop) {
            width: 100px;
            height: 12px;
          }
        }
      }
      .square-group {
        position: absolute;
        bottom: 0;
        right: 4px;
        @include rwdmin($desktop) {
          bottom: -10px;
        }
        .square {
          @include rwdmax($tablet - 1) {
            width: 30px;
            height: 30px;
          }
          @include rwd($tablet, $desktop - 1) {
            width: 44px;
            height: 44px;
          }
          @include rwdmin($desktop) {
            width: 82px;
            height: 82px;
          }
          &:first-child {
            background-color: $orange;
            position: relative;
            z-index: 1;
          }
          &:last-child {
            background-color: $deep-brown;
            position: absolute;
            bottom: -12px;
            left: -12px;
            @include rwdmin($desktop) {
              bottom: -25px;
              left: -25px;
            }
          }
        }
      }
    }
  }
}
</style>
