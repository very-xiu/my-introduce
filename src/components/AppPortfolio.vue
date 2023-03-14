<template>
  <section class="portfolio section" id="portfolio">
    <h2 class="section__title">{{ $t("portfolio__title") }}</h2>
    <span class="section__subtitle">{{ $t("portfolio__subtitle") }}</span>

    <div class="portfolio__container container swiper-container">
      <swiper
        class="swiper"
        :modules="modules"
        :slides-per-view="1"
        :space-between="30"
        :loop="true"
        :autoplay="{
          pauseOnMouseEnter: true,
          disableOnInteraction: false,
          delay: 3000,
        }"
        :pagination="{ clickable: true }"
        navigation
      >
        <swiper-slide v-for="(item, index) in portfolioList" :key="index">
          <div class="portfolio__content grid swiper-slide">
            <img :src="item.img" alt="" class="portfolio__img" />

            <div class="portfolio_">
              <h3 class="portfolio__title" i18n="portfolio1__title">
                {{ $t(item.title) }}
              </h3>
              <p class="portfolio__description" i18n="portfolio1__description">
                {{ $t(item.describe) }}
              </p>
              <a
                :href="item.url"
                target="_blank"
                class="button button--flex button--small portfolio__button"
              >
                {{ $t("works__text") }}
                <i class="alicon alicon-zhixiangyou button__icon"></i>
              </a>
            </div>
          </div>
        </swiper-slide>
      </swiper>
    </div>
  </section>
</template>
<script>
import { defineComponent, ref } from "vue";
import { Pagination, Navigation,Autoplay } from "swiper";
import { Swiper, SwiperSlide } from "swiper/vue";
import { useThemeState } from "@/store";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";

export default defineComponent({
  name: "AppPortfolio",
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    const state = useThemeState();
    const portfolioList = ref([
      {
        url: state.worksUrl + "?type=react",
        title: "portfolio1__title",
        describe: "portfolio1__description",
        img: require("@/assets/img/1659266697694.png"),
      },
      {
        url: state.worksUrl + "?type=min",
        title: "portfolio2__title",
        describe: "portfolio2__description",
        img: require("@/assets/img/惠州保障房小程序.jpg"),
      },
      {
        url: state.worksUrl + "",
        title: "portfolio3__title",
        describe: "portfolio3__description",
        img: require("@/assets/img/智慧律所-立项流程.png"),
      },
    ]);
    return {
      modules: [Pagination, Navigation,Autoplay],
      portfolioList,
    };
  },
});
</script>

<style lang="scss" scoped>
.portfolio {
  &__container {
    overflow: initial;
  }

  &__content {
    padding: 0 1.5rem;
    @include min-screen(568px) {
      grid-template-columns: repeat(2, 1fr);
    }
    @include min-screen(768px) {
      align-items: center;
    }
    @include min-screen(1024px) {
      column-gap: 5rem;
    }
  }
  :deep(.swiper-wrapper) {
    margin-bottom: 2.5rem;
  }
  :deep(.swiper-button-prev) {
    @include max-screen(768px) {
      left: -5px;
      top: 23%;
    }
  }
  :deep(.swiper-button-next) {
    @include max-screen(768px) {
      right: -5px;
      top: 23%;
    }
  }
  &__img {
    // width: 265px;
    height: 145px;
    width: auto;
    border-radius: 0.5rem;
    justify-self: center;
    @include min-screen(768px) {
      // width: 320px;
      height: 165px;
      width: auto;
    }
  }

  &__title {
    font-size: var(--h3-font-size);
    margin-bottom: var(--mb-0-5);
  }

  &__description {
    margin-bottom: var(--mb-0-75);
    padding-right: 0.65rem;
  }

  &__button:hover .button__icon {
    transform: translateX(0.25rem);
  }
}
::v-deep .swiper-button-next:after,
::v-deep .swiper-button-prev:after {
  font-size: 1.5rem;
  color: var(--first-color);
}
::v-deep .swiper-pagination-bullet-active {
  background-color: var(--first-color);
}
</style>
