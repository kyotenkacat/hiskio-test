<template>
  <div id="hot-lesson">
    <div class="section-title">
      <div class="title-decor">
        <span class="dot"></span>
        <span class="dot"></span>
        <span class="dot"></span>
      </div>
      <div class="title-content-container">
        <div class="title-content">
          <p>你不能錯過的熱門課程，為未來充點值!</p>
          <button
            v-for="item in categories"
            :key="item"
            :class="{ selected: selectedItem === item }"
            @click="selectedItem = item"
          >
            {{ item }}
          </button>
        </div>
      </div>
    </div>
    <div class="carousel">
      <div class="carousel-inner">
        <div
          v-for="(slider, key) in lessonList"
          :key="key"
          class="carousel-item"
          :class="{
            selected: selectedItem === key,
            'slide-to-left': slideToLeft && selectedItem === key,
            'slide-to-right': slideToRight && selectedItem === key,
          }"
        >
          <div v-for="(lesson, index) in slider" :key="index" class="lesson">
            <div class="info">
              <div class="title">
                <p>
                  <span v-if="lesson.title.preTitle">
                    {{ lesson.title.preTitle }}
                  </span>
                  <span class="main">{{ lesson.title.title }}</span>
                </p>
                <p>{{ lesson.title.subTitle }}</p>
              </div>
              <div class="number-info">
                <div class="teacher left-col">
                  <img
                    :src="require(`@/assets/teacher-${lesson.teacher.id}.png`)"
                    :alt="`${lesson.teacher.name}`"
                  />
                  <span>{{ lesson.teacher.name }}</span>
                </div>
                <div class="student right-col">
                  <img src="@/assets/student.png" alt="student-icon" />
                  <span>超過 {{ lesson.studentCount }} 人</span>
                </div>
                <div class="price left-col">
                  原價 <span> ${{ lesson.price.original }}</span>
                </div>
                <div class="price right-col">
                  <span>${{ lesson.price.sale }}</span>
                </div>
              </div>
            </div>
            <div class="comment">
              <div class="star">
                <img
                  v-for="num in [1, 2, 3, 4, 5]"
                  :key="num"
                  src="@/assets/star.png"
                  alt="star"
                />
              </div>
              <div class="word">{{ lesson.comment }}</div>
              <div class="btn-group">
                <button><p>看看課程</p></button>
                <button><p>加入購物車</p></button>
              </div>
            </div>
            <img
              :src="require(`@/assets/logo/${lesson.logo}.png`)"
              class="logo"
              :class="`logo-${index}`"
              :alt="`${lesson.logo}-logo`"
            />
            <img
              v-if="index === 0"
              :src="
                require(`@/assets/${
                  devicePath === 'mobile' ? 'mobile' : 'desktop'
                }/long-firecracker.png`)
              "
              class="long-firecracker"
              alt="firecracker"
            />
            <img
              v-if="index === 1"
              src="@/assets/firecracker.png"
              class="firecracker"
              alt="firecracker"
            />
          </div>
        </div>
        <button
          class="arrow arrow-left"
          :disabled="selectedItem === categories[0]"
          @click="slide('left')"
        >
          <img src="@/assets/arrow-left.png" alt="arrow-left" />
        </button>
        <button
          class="arrow arrow-right"
          :disabled="selectedItem === categories[categories.length - 1]"
          @click="slide('right')"
        >
          <img src="@/assets/arrow-right.png" alt="arrow-right" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { inject } from 'vue';

export default {
  name: 'HotLesson',
  setup() {
    const devicePath = inject('devicePath');

    return {
      devicePath,
    };
  },
  data() {
    return {
      categories: ['前端', '接案', '後端', '雲端'],
      selectedItem: '前端',
      lessonList: {
        前端: [
          {
            title: {
              preTitle: null,
              title: 'Vue.js',
              subTitle: '前端開發完全指南',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 1200,
            price: {
              original: 3200,
              sale: 2176,
            },
            comment: '謝謝姚老師，我以前都用 JQ 開發，想換工作所以自學新框架，想說學 Vue 看看，沒想到用照著老師的影片練習很快就寫出瀑布流的效果了！真的很開心！',
            logo: 'vue',
          },
          {
            title: {
              preTitle: '【完全精通】',
              title: 'React 16',
              subTitle: '從原理到大量實戰應用',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 566,
            price: {
              original: 3200,
              sale: 2176,
            },
            comment: '網路上比較了幾間教學內容，甚至問了會 React 的朋友，都推說這個老師教學內容比較多，可以買看看，看了課程後很慶幸自己買對了！',
            logo: 'react',
          },
        ],
        接案: [
          {
            title: {
              preTitle: null,
              title: 'WordPress',
              subTitle: '主題開發 2大專案帶你打造4大版型',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 150,
            price: {
              original: 2500,
              sale: 1700,
            },
            comment: '對 WordPress 有很大的興趣但又不知如何下手，坊間書籍看了只會基本的架設，感謝老師從實例來探討，讓我能得心應手的使用 WordPress 來接案！',
            logo: 'wordPress',
          },
          {
            title: {
              preTitle: null,
              title: 'JavaScript',
              subTitle: '三大專案帶你輕鬆入門',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 300,
            price: {
              original: 3000,
              sale: 2040,
            },
            comment: '用一個完整的實作一步一步來帶學員從中學習，然後再一邊講解的方式，我覺得很不錯，學完能清楚某些功能應該用在哪邊！',
            logo: 'js',
          },
        ],
        後端: [
          {
            title: {
              preTitle: null,
              title: 'Django+Flask',
              subTitle: '雙框架實戰 從新手到業界職人',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 350,
            price: {
              original: 4800,
              sale: 3264,
            },
            comment: '整體來說相當實用，課程內容不只包含 Django 的基本觀念，亦涵蓋進階用法及實際部署流程，如: SSL 、Docker 打包、GCP 部署',
            logo: 'django',
          },
          {
            title: {
              preTitle: null,
              title: 'NUXT.js',
              subTitle: '前端開發實戰手冊',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 300,
            price: {
              original: 3500,
              sale: 2380,
            },
            comment: '覺得這個課程內容還蠻多元的，像是基於 Vue 的 Nuxt 開發、Node API 建立串接、自動環境佈署，從前端延續到後端的開發應用，非常不錯的課程！',
            logo: 'nuxt',
          },
        ],
        雲端: [
          {
            title: {
              preTitle: '圖解',
              title: 'AWS+GCP',
              subTitle: '雲端雙平台入門完全指南',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 350,
            price: {
              original: 3800,
              sale: 2645,
            },
            comment: '講解得非常常清楚，搭配圖片深入淺出的了解 AWS 與 GCP 的基本概念與操作，省下很多自己研究的時間！',
            logo: 'aws',
          },
          {
            title: {
              preTitle: null,
              title: 'Kubernetes',
              subTitle: '實作手冊 基礎入門篇',
            },
            teacher: {
              id: 621,
              name: '姚偉揚',
            },
            studentCount: 350,
            price: {
              original: 3900,
              sale: 2652,
            },
            comment: '老師的語意表達清晰，口條清楚，課程從理論 ( Docker / K8S ) 到實作，以及後續的 Debug，這堂課程很值得學習！',
            logo: 'kubernetes',
          },
        ],
      },
      slideToLeft: false,
      slideToRight: false,
    };
  },
  methods: {
    slide(type) {
      const index = this.categories.findIndex((item) => item === this.selectedItem);
      let newIndex;
      if (type === 'left') {
        newIndex = index - 1 >= 0 ? index - 1 : index;
        this.slideToLeft = true;
        this.slideToRight = false;
      } else {
        newIndex = index + 1 < this.categories.length ? index + 1 : index;
        this.slideToRight = true;
        this.slideToLeft = false;
      }
      this.selectedItem = this.categories[newIndex];
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/variables.scss";

#hot-lesson {
  .section-title {
    position: relative;
    z-index: 1;
    .title-content {
      button {
        border-radius: 50%;
        border: 2px solid $brown;
        position: relative;
        color: $deep-brown;
        margin: 0 3%;
        background: none;
        @include rwdmax($desktop - 1) {
          width: 56px;
          height: 56px;
        }
        @include rwdmin($desktop) {
          width: 90px;
          height: 90px;
        }
        &.selected {
          background-color: $yellow;
        }
        &:before {
          display: block;
          content: "";
          border-radius: 50%;
          border: 2px solid $brown;
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          @include rwdmax($desktop - 1) {
            width: 46px;
            height: 46px;
          }
          @include rwdmin($desktop) {
            width: 74px;
            height: 74px;
          }
        }
        @include rwdmax($desktop - 1) {
          font-size: 18px;
        }
        @include rwdmin($desktop) {
          font-size: 28px;
        }
      }
    }
  }
  .carousel {
    background-color: $gray;
    margin-top: -50px;
    .carousel-inner {
      position: relative;
      overflow: hidden;
      @include rwdmax($tablet - 1) {
        padding: 65px 0;
      }
      @include rwdmin($tablet) {
        padding: 100px 0 65px;
      }
    }
    .carousel-item {
      display: inline-block;
      width: 100%;
      margin-right: -100%;
      visibility: hidden;
      backface-visibility: hidden;
      &.selected {
        visibility: visible;
      }
      &.slide-to-left {
        animation: slideToLeft 0.6s;
      }
      &.slide-to-right {
        animation: slideToRight 0.6s;
      }
    }
  }
  .lesson {
    background-color: $brown;
    position: relative;
    padding-bottom: 15px;
    &:first-child {
      @include rwdmax($tablet - 1) {
        margin: 0 20px 50px 0;
        padding-left: 56px;
      }
      @include rwd($tablet, $desktop - 1) {
        margin: 0 120px 50px 0;
        padding: 10px 10px 10px 135px;
        display: flex;
        align-items: center;
      }
      @include rwdmin($desktop) {
        margin: 0 27% 70px 0;
        padding: 20px 20px 20px 27%;
        display: flex;
        align-items: center;
      }
    }
    &:nth-child(2) {
      @include rwdmax($tablet - 1) {
        margin-left: 20px;
        padding-left: 56px;
      }
      @include rwd($tablet, $desktop - 1) {
        margin-left: 120px;
        padding: 10px 90px 10px 10px;
        display: flex;
        align-items: center;
        flex-flow: row-reverse;
        .info {
          padding-left: 15px;
        }
      }
      @include rwdmin($desktop) {
        margin-left: 27%;
        padding: 20px 27% 20px 20px;
        display: flex;
        align-items: center;
        flex-flow: row-reverse;
        .info {
          padding-left: 25px;
        }
      }
    }
    p {
      margin: 0;
    }
    .info {
      @include rwd($tablet, $desktop - 1) {
        width: 50%;
      }
      @include rwdmin($desktop) {
        width: 60%;
      }
    }
    .title {
      color: #fff;
      font-weight: bold;
      line-height: 1.5;
      p {
        @include rwdmax($tablet - 1) {
          font-size: 18px;
        }
        @include rwd($tablet, $desktop - 1) {
          font-size: 22px;
        }
        @include rwdmin($desktop) {
          font-size: 28px;
        }
        .main {
          @include rwdmax($tablet - 1) {
            font-size: 30px;
          }
          @include rwd($tablet, $desktop - 1) {
            font-size: 22px;
          }
          @include rwdmin($desktop) {
            font-size: 28px;
          }
        }
      }
    }
    .number-info {
      @include rwdmax($tablet - 1) {
        margin-top: 5px;
      }
      .left-col,
      .right-col {
        display: inline-block;
        vertical-align: middle;
      }
      .left-col {
        @include rwdmax($tablet - 1) {
          width: 30%;
        }
        @include rwdmin($tablet) {
          width: 40%;
        }
      }
      .right-col {
        @include rwdmax($tablet - 1) {
          width: 70%;
        }
        @include rwdmin($tablet) {
          width: 60%;
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
      .price {
        &.left-col {
          color: $deep-brown;
          span {
            text-decoration: line-through;
          }
        }
        &.right-col {
          span {
            color: $yellow;
            @include rwdmax($desktop - 1) {
              font-size: 26px;
            }
            @include rwdmin($desktop) {
              font-size: 28px;
            }
          }
        }
      }
      .teacher,
      .student {
        img {
          vertical-align: middle;
          margin-right: 5px;
          @include rwdmax($tablet - 1) {
            width: 30px;
          }
          @include rwd($tablet, $desktop - 1) {
            width: 22px;
          }
          @include rwdmin($desktop) {
            width: 28px;
          }
        }
        span {
          vertical-align: middle;
          color: $deep-brown;
        }
      }
    }
    .comment {
      padding: 4px 10px 20px;
      margin-top: 5px;
      background-color: $gray;
      box-shadow: 5px 5px $deep-brown;
      text-align: center;
      color: $deep-brown;
      position: relative;
      @include rwdmax($tablet - 1) {
        width: 94%;
      }
      @include rwd($tablet, $desktop - 1) {
        width: 50%;
      }
      @include rwdmin($desktop) {
        width: 40%;
      }
      .star {
        margin-bottom: 2px;
        img {
          width: 12px;
          margin-right: 1px;
        }
      }
      .word {
        @include rwdmax($desktop - 1) {
          font-size: 16px;
        }
        @include rwdmin($desktop) {
          font-size: 20px;
        }
      }
      .btn-group {
        width: 100%;
        position: absolute;
        top: 90%;
        left: 50%;
        transform: translateX(-50%);
        button {
          background-color: $yellow;
          padding: 4px;
          border: 1px solid $brown;
          @include rwdmax($tablet - 1) {
            width: 35%;
          }
          @include rwdmin($tablet) {
            width: 40%;
          }
          &:first-child {
            margin-right: 20px;
          }
          p {
            padding: 8px 2px;
            border: 1px solid $brown;
            color: $deep-brown;
            @include rwdmax($desktop - 1) {
              font-size: 18px;
            }
            @include rwdmin($desktop) {
              font-size: 20px;
            }
          }
        }
      }
    }
    .logo {
      position: absolute;
      &.logo-0 {
        top: 0px;
        left: -12px;
        @include rwdmax($tablet - 1) {
          width: 70px;
        }
        @include rwd($tablet, $desktop - 1) {
          width: 140px;
        }
        @include rwdmin($desktop) {
          width: 190px;
          left: 20%;
        }
      }
      &.logo-1 {
        @include rwdmax($tablet - 1) {
          width: 90px;
          top: 0px;
          right: -6px;
        }
        @include rwd($tablet, $desktop - 1) {
          width: 155px;
          bottom: 0;
          right: -6px;
        }
        @include rwdmin($desktop) {
          width: 200px;
          bottom: 0;
          right: 20%;
        }
      }
    }
    .long-firecracker {
      position: absolute;
      top: 0;
      @include rwdmax($tablet - 1) {
        width: 40px;
        right: -20px;
      }
      @include rwdmin($tablet) {
        width: 154px;
        transform: translateY(-50%);
        left: 0px;
      }
      @include rwdmin($desktop) {
        width: 20%;
      }
    }
    .firecracker {
      position: absolute;
      width: 44px;
      bottom: 0;
      @include rwdmax($tablet - 1) {
        width: 44px;
        left: -16px;
      }
      @include rwdmin($tablet) {
        width: 24px;
        right: 10px;
      }
      @include rwdmin($desktop) {
        width: 5%;
        right: 15%;
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
}

@keyframes slideToRight {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0%);
  }
}
@keyframes slideToLeft {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0%);
  }
}
</style>
