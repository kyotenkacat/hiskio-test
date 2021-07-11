<template>
  <div id="red-envelope">
    <div class="lion-container">
      <div class="img-container">
        <img src="@/assets/lion.png" alt="lion" />
      </div>
      <div class="talk-continer">
        <img
          :src="
            require(`@/assets/${
              devicePath === 'mobile' ? 'mobile' : 'desktop'
            }/talking-cloud.png`)
          "
          alt="talking-cloud"
        />
        <span>三種紅包領好領滿，錯過領券時間就沒有囉！</span>
      </div>
    </div>
    <div class="envelop-container">
      <div class="timeline">
        <div class="date">
          <span>1/18</span>
          <span>2/1 23:59</span>
          <span>2/8 23:59</span>
          <span>2/15</span>
        </div>
        <div class="coin">
          <div v-for="item in [1, 2, 3, 4]" :key="item" class="img-container" />
        </div>
      </div>
      <div class="envelope-list">
        <div class="envelope">
          <img
            :src="
              require(`@/assets/${
                devicePath === 'mobile' ? 'mobile' : 'desktop'
              }/envelope-past.png`)
            "
            alt="envelope-past"
          />
          <p class="type">
            <span class="number">68</span>
            <span class="word">折</span>
          </p>
          <p v-if="devicePath !== 'mobile'" class="hint">
            不限訂單金額皆可使用，領券7天內使用完畢
          </p>
        </div>
        <div class="envelope">
          <img
            :src="
              require(`@/assets/${
                devicePath === 'mobile' ? 'mobile' : 'desktop'
              }/envelope-now.png`)
            "
            alt="envelope-now"
          />
          <p class="type">
            <span class="number">500</span>
            <span class="word">元</span>
          </p>
          <p v-if="devicePath !== 'mobile'" class="hint">
            訂單超過$2500可使用，領券30天內使用完畢
          </p>
        </div>
        <div class="envelope">
          <img
            :src="
              require(`@/assets/${
                devicePath === 'mobile' ? 'mobile' : 'desktop'
              }/envelope-future.png`)
            "
            alt="envelope-future"
          />
          <p class="type">
            <span class="number">?</span>
          </p>
        </div>
        <div v-if="devicePath === 'mobile'" class="hint-container">
          <p>
            <img src="@/assets/mobile/ingots.png" alt="ingots" />
            <span>68 折券：不限訂單金額，領券 7 天內使用</span>
          </p>
          <p>
            <img src="@/assets/mobile/ingots.png" alt="ingots" />
            <span>500 元券：訂單滿 $2500，領券 30 天內使用</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, inject } from 'vue';

export default defineComponent({
  name: 'RedEnvelope',
  setup() {
    const devicePath = inject('devicePath');

    return {
      devicePath,
    };
  },
  data() {
    return {
    };
  },
});
</script>

<style lang="scss" scoped>
@import "@/styles/variables.scss";

#red-envelope {
  @include rwdmax($tablet - 1) {
    margin: 25px 0;
  }
  @include rwd($tablet, $desktop - 1) {
    margin: 50px 0;
  }
  @include rwdmin($desktop) {
    margin: 160px 0;
  }
  .lion-container {
    display: flex;
    justify-content: center;
    .img-container {
      @include rwdmax($tablet - 1) {
        width: 80px;
        margin-right: 10px;
      }
      @include rwd($tablet, $desktop - 1) {
        width: 95px;
        margin-right: 10px;
      }
      @include rwdmin($desktop) {
        width: 132px;
        margin-right: 15px;
      }
      img {
        width: 100%;
      }
    }
    .talk-continer {
      position: relative;
      display: flex;
      align-items: center;
      @include rwdmax($tablet - 1) {
        width: 225px;
        padding: 0 22px 10px;
      }
      @include rwd($tablet, $desktop - 1) {
        width: 500px;
        padding: 0 30px;
      }
      @include rwdmin($desktop) {
        max-width: 662px;
        width: 660px;
        padding: 0 42px;
      }
      span {
        color: $deep-brown;
        @include rwdmax($tablet - 1) {
          font-size: 18px;
        }
        @include rwd($tablet, $desktop - 1) {
          font-size: 22px;
        }
        @include rwdmin($desktop) {
          font-size: 28px;
        }
      }
      img {
        width: 100%;
        display: inline;
        position: absolute;
        top: 0;
        left: 0;
        z-index: -1;
        box-shadow: 5px 5px $deep-brown;
        @include rwdmin($tablet) {
          top: 50%;
          transform: translateY(-50%);
        }
      }
    }
  }
  .envelop-container {
    color: $deep-brown;
    @include rwdmax($tablet - 1) {
      padding: 15px;
    }
    @include rwd($tablet, $desktop - 1) {
      padding: 15px 70px;
    }
    @include rwdmin($desktop) {
      padding: 40px 15%;
    }
    .timeline {
      width: 100%;
      .date {
        display: flex;
        justify-content: space-between;
        @include rwdmax($tablet - 1) {
          font-size: 16px;
        }
        @include rwd($tablet, $desktop - 1) {
          font-size: 16px;
        }
        @include rwdmin($desktop) {
          font-size: 26px;
        }
      }
      .coin {
        display: flex;
        justify-content: space-between;
        margin-top: 4px;
        position: relative;
        &:before {
          width: 100%;
          display: block;
          content: "";
          background-color: $brown;
          position: absolute;
          top: 50%;
          z-index: -1;
          @include rwdmax($tablet - 1) {
            height: 2px;
          }
          @include rwd($tablet, $desktop - 1) {
            height: 3px;
          }
          @include rwdmin($desktop) {
            height: 4px;
          }
        }
        .img-container {
          @include rwdmax($tablet - 1) {
            width: 28px;
            height: 28px;
          }
          @include rwd($tablet, $desktop - 1) {
            width: 32px;
            height: 32px;
          }
          @include rwdmin($desktop) {
            width: 55px;
            height: 55px;
          }
          background-size: contain;
          &:first-child,
          &:last-child {
            background-image: url("~@/assets/coin-gray.png");
          }
          &:nth-child(2),
          &:nth-child(3) {
            background-image: url("~@/assets/coin-gold.png");
          }
        }
      }
    }
    .envelope-list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-evenly;
      .envelope {
        width: 28%;
        position: relative;
        img {
          width: 100%;
        }
        p {
          color: $beige;
          position: absolute;
          margin: 0;
        }
        .type {
          left: 0;
          right: 0;
          text-align: center;
          @include rwdmax($tablet - 1) {
            top: 50%;
          }
          @include rwdmin($tablet) {
            top: 45%;
          }
          .number {
            @include rwdmax($desktop - 1) {
              font-size: 36px;
            }
            @include rwdmin($desktop) {
              font-size: 62px;
            }
          }
          .word {
            @include rwdmax($desktop - 1) {
              font-size: 16px;
            }
            @include rwdmin($desktop) {
              font-size: 34px;
            }
          }
        }
        .hint {
          bottom: 12%;
          line-height: 1.5;
          padding: 0 20px;
          text-align: center;
          @include rwdmax($desktop - 1) {
            font-size: 12px;
          }
          @include rwdmin($desktop) {
            font-size: 20px;
          }
        }
      }
      .hint-container {
        width: 100%;
        color: $deep-brown;
        font-size: 12px;
        line-height: 1.5;
        padding: 18px 0 0 50px;
        p {
          margin: 0;
        }
        img {
          width: 16px;
          margin-right: 2px;
        }
      }
    }
  }
}
</style>
