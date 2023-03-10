<template>
  <div class="all">
    <p class="title">關鍵字觀察室</p>
    <p class="subtitle">關於『 關鍵字 』的最新新聞</p>

    <div class="section_layout">
      <!-- 左側區域 -->
      <div class="section_left">
        <div v-for="(item, index) in news" :key="index">
          <a class="keyword_layout" :href="'https://www.ftvnews.com.tw/news/detail/' + item.ID" target="_blank">
            <p class="keyword_title_no"> {{ index + 1 }}.</p>
            <div class="keyword_inner">
              <div class="keyword_left">
                <img :src="item.Image" class="keyword_img" alt="新聞照片">
              </div>

              <div class="keyword_right">
                <h2 class="keyword_title">
                  {{ item.Title }}</h2>
                <p class="keyword_content">
                  針對美國政府於美東時間3月1日就「AGM-88B、AIM-120C」等2型飛彈，金額6億1,900萬美元對台軍售案進行「知會國會」程序並可望在1個月後正式生效，總統府發言人Kolas
                  Yotaka今（2）日表示，總統府再次感謝美國政府依照「台灣關係法」與「六項保證」精神，維持區域安全穩定，落實對台灣強化自我防禦能力的承諾。</p>
                <p class="keyword_time">
                  {{ item.CreateDate }}</p>
              </div>
            </div>
          </a>
        </div>
      </div>
      <!-- 左側區域end -->
      <!-- 右側區域 -->
      <div class="section_right">
        <!-- 相關議題 start -->
        <div class="related_layout">
          <h3><i class="fa-solid fa-tags"></i>相關議題</h3>
          <div class="hashtag_layout">
            <ul class="hashtag" v-for="(item, index) in 8" :key="index">
              <li>相關標籤</li>
            </ul>
          </div>
        </div>
        <!-- 相關議題end -->
        <!-- 更多搜尋結果 start -->
        <div class="Serp_layout">
          <h3><i class="fa-solid fa-magnifying-glass"></i>更多熱搜結果</h3>
          <div class="Serp_inner" v-for="(item, index) in 10" :key="index">
            <a href="#" target="_blank" v-if="index < 10">
              <p class="Serp_title">
                {{ index + 1 }}.Google搜尋結果Google搜尋結果Google搜尋結果Google搜尋結果Google搜尋結果Google搜尋結果
              </p>
              <p class="Serp_content">
                Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容
                Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容</p>
            </a>
          </div>
        </div>
        <!-- 更多搜尋結果 end -->
      </div>
      <!-- 右側區域end -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      news: [],
    }
  },
  methods: {
    text() {
      this.axios
        .get("https://ftvnews-api2.azurewebsites.net/API/FtvGetNewsWeb.aspx?Cate=政治&Page=1&sp=15")
        .then((response) => {
          // console.log('news', response)
          let data = response.data.ITEM
          data.forEach((item) => { this.news.push(item) })
        })
        .catch((error) => {
          console.log("error" + error);
        });

    },
  },
  mounted() {
    this.text();
  }
}
</script>
<style scoped>
@import "../css/style.css";
</style>