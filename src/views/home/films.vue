<template>
  <van-list
    v-model="filmLoading"
    @load="getFilmList"
    :finished="isFinished"
    finished-text="别拉了"
    ref="myBox"
  >
    <div class="page-home-films">
      <Banner class="banner" :list="bannerList" pagination loop />

      <div class="city-fixed" @click="handleGoCity">
        <span>{{ curCityInfo && curCityInfo.name }}</span>
        <i class="iconfont icon-xiala"></i>
      </div>

      <van-tabs v-model="curFilmType" sticky>
        <van-tab title="正在热映">
          <Filmlist filmType="nowPlaying" :list="filmList" />
        </van-tab>
        <van-tab title="即将上映">
          <Filmlist filmType="comingSoon" :list="filmList" />
        </van-tab>
      </van-tabs>
    </div>
  </van-list>
</template>

<script>
import Banner from "@/components/Banner";
import Filmlist from "@/components/Filmlist";
import { mapState, mapGetters, mapActions } from "vuex";

export default {
  name: "films",

  components: {
    Banner,
    Filmlist
  },

  /*   data() {
    return {
      active: 0
    }
  }, */

  computed: {
    ...mapState("film", ["bannerList", "filmList"]),
    ...mapGetters("film", ["isFinished"]),
    ...mapGetters("city", ["curCityInfo"]),

    curFilmType: {
      get() {
        return this.$store.state.film.curFilmType;
      },

      set(value) {
        this.$store.commit({
          type: "film/setCurFilmType",
          filmType: value
        });
      }
    },

    filmLoading: {
      get() {
        return this.$store.state.film.filmLoading;
      },

      set(value) {
        this.$store.commit({
          type: "film/setFilmLoading",
          loading: value
        });
      }
    }
  },
  watch: {
    curFilmType(newVal, oldVal) {
      this.$refs.myBox.$el.scrollTop = 0;
      this.getFilmList(true);
    }
  },

  methods: {
    ...mapActions("film", ["getBannerList", "getFilmList"]),

    //跳到城市页面
    handleGoCity() {
      this.$router.push("/city");
    }
  },

  created() {
    this.getBannerList();
  }
};
</script>

<style lang="scss">
.page-home-films {
  .banner {
    img {
      width: 100%;
    }
  }
  .city-fixed {
    position: absolute;
    top: 18px;
    left: 7px;
    color: #fff;
    z-index: 10;
    font-size: 13px;
    background: rgba(0, 0, 0, 0.2);
    height: 30px;
    line-height: 30px;
    border-radius: 15px;
    text-align: center;
    padding: 0 5px;

    i {
      font-size: 10px;
    }
  }
}
</style>
