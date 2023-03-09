<template>
  <div class="all" id="hotnews">
    <p class="hot_title">關鍵字觀察室</p>
    <p class="hot_news_subtitle">關於『 關鍵字 』的最新新聞</p>
    <div class="hot_news">
      <!-- 關於『 關鍵字 』的最新新聞15 -->
      <div class="news_right">
        <div v-for="(item, index) in news" :key="index">
          <a class="keyword_layout" :href="'https://www.ftvnews.com.tw/news/detail/' + item.ID" target="_blank">
            <p class="title_no"> {{ index + 1 }}.</p>
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
      <div class="cand_right">
        <div class="Serp_layout">
          <h3><i class="fa-solid fa-tags"></i>相關議題</h3>
          <div class="hashtag_layout">
            <div class="hashtag" v-for="(item, index) in 8" :key="index">
              <p>相關標籤</p>
            </div>
          </div>
        </div>
        <div class="Serp_layout2">
          <h3><i class="fa-solid fa-magnifying-glass"></i>更多熱搜結果</h3>
          <div class="Serp_inner" v-for="(item, index) in 10" :key="index">
            <a href="#" target="_blank" v-if="index < 10">
              <!-- 最多兩行 -->
              <p class="Serp_title">
                {{ index + 1 }}.Google搜尋結果Google搜尋結果Google搜尋結果Google搜尋結果Google搜尋結果Google搜尋結果
              </p>
              <p class="Serp_content">
                Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容
                Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容Google搜尋內容</p>
            </a>
          </div>
        </div>
      </div>
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
    get_news() {
      // eslint-disable-next-line no-undef
      this.axios
        .get("https://ftvnews-api2.azurewebsites.net/API/FtvGetNewsWeb.aspx?Cate=政治&Page=1&sp=15")
        .then((response) => {
          console.log('ssss', response)
          let data = response.data.ITEM
          data.forEach((item) => { this.news.push(item) })
        })
        .catch((error) => {
          console.log("error" + error);
        });

    },
  },
  mounted() {
    this.get_news();
  }
}
</script>

<style lang="scss">
$shadow: 6px 14px 36px rgba(48, 58, 73, 0.06), 1px 4px 8px rgba(48, 58, 73, 0.04);
$blue: #1b31b9;


.fa-solid {
  margin: .5rem;
  color: $blue;
}

.all {
  background: #f5f7f9;
}

.title_no {
  font-size: 2rem;
  margin: 1rem .5rem;
  font-weight: 600;
}

@media screen and (max-width: 768px) {
  .title_no {
    font-size: 1.2rem;
    font-weight: 600;
    margin-left: 1rem;
    margin-right: 0rem;
  }

}

.keyword_title {
  text-align: left;
  display: -webkit-box;
  line-height: 1.4;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
  overflow: hidden;
}

.keyword_inner {
  display: grid;
  grid-template-columns: 1fr 4fr;
  background: white;
  margin: .8rem;
  border-radius: 10px;
  box-shadow: $shadow;
}

@media screen and (max-width: 900px) {
  .keyword_inner {
    grid-template-columns: 1fr 5fr;

  }
}

@media screen and (max-width: 768px) {

  .keyword_inner {
    grid-template-columns: 1fr 2fr;
    margin: 1rem 1rem 0rem 1rem;
  }

}

.keyword_layout {
  display: flex;
}


.keyword_right {
  margin: 1rem
}



@media screen and (max-width: 768px) {
  .keyword_right {
    margin: .5rem 1rem;
    font-size: .8rem;
  }
}

.keyword_content {
  margin: 1.5rem auto 1rem;
  text-align: left;
  font-size: 1.2rem;
  display: -webkit-box;
  line-height: 1.5;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
  color: rgb(87, 87, 87)
}


@media screen and (max-width: 900px) {
  .keyword_content {
    -webkit-line-clamp: 2;
  }

}

@media screen and (max-width: 768px) {
  .keyword_content {
    margin: .5rem auto;
    font-size: 1rem;
  }
}

.keyword_time {
  display: flex;
  justify-content: end;
  color: rgb(87, 87, 87);
  margin: 0;
  align-items: end;
}

.keyword_img {
  width: 320px;
  height: 220px;
  object-fit: cover;
  border-radius: 10px 0 0 10px;
  margin-bottom: -6px;
}

@media screen and (max-width: 900px) {
  .keyword_img {
    width: 230px;
    height: 190px;
    object-fit: cover;
    border-radius: 10px 0 0 10px;
    margin-bottom: -6px;
  }
}

@media screen and (max-width: 768px) {
  .keyword_img {
    width: 100%;
    height: 130px;
  }
}

@media screen and (max-width: 500px) {
  .keyword_img {
    height: 130px;
  }
}



.hot_title {
  text-align: start;
  font-size: 48px;
  font-weight: bold;
  margin-left: 56px;
  letter-spacing: .3rem;
}

.hot_news_subtitle {
  text-align: start;
  font-size: 24px;
  margin: 0;
  margin-left: 57px;
}

@media screen and (max-width: 768px) {
  .hot_title {
    text-align: start;
    font-size: 1.4rem;
    margin: .2rem 1rem;
    margin-left: 57px;
    margin-top: 1rem;
  }

  .hot_news_subtitle {
    text-align: start;
    font-size: 1rem;
    margin: 0rem 1rem;
    margin-left: 57px;
  }

}



.Serp_title {
  text-align: start;
  display: -webkit-box;
  line-height: 1.4;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
  font-size: 1.2rem;
  font-weight: 600;
  margin: 1rem 0rem;
}

.Serp_inner {
  margin: 2rem 0rem
}

.Serp_layout {
  margin: auto;
  padding: 1rem;
  background: white;
  border-radius: 10px;
  box-shadow: $shadow
}

.Serp_layout2 {
  margin: auto;
  padding: 1rem;
  background: white;
  border-radius: 10px;
  box-shadow: $shadow;
  margin-top: 1.5rem
}

@media screen and (max-width: 768px) {

  .Serp_layout {
    margin: 1rem;
  }

  .Serp_layout2 {
    margin: 2rem 1rem;
  }

}

.Serp_content {
  text-align: start;
  display: -webkit-box;
  line-height: 1.4;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 4;
  overflow: hidden;
  color: rgb(87, 87, 87)
}


.hot_news_img {
  border-radius: 5px;
  width: 300px;
  height: 200px;
  object-fit: cover;
  margin: auto;
}



.hot_news_inner {
  display: grid;
  grid-template-columns: 1fr 3fr;
  background: white;
  border-radius: 10px;
  padding: 1rem;
  margin: 1rem;
  filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.15));
  text-align: left;
}


.hot_news {
  max-width: 1600px;
  display: grid;
  margin: auto;
  grid-template-columns: 5fr 1fr;
  position: relative;
  gap: 1rem;
  margin: 0rem 1rem;
}

@media screen and (max-width: 768px) {
  .hot_news {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: 0rem;
  }

}


.news_left {
  margin: 0.5rem 1rem;
}


.hot_news_title {

  display: inline-block;
  display: -webkit-box;
  line-height: 1.4;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}

.hot_news_content {

  display: inline-block;
  display: -webkit-box;
  line-height: 1.4;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;

}


.hot_news_right {
  display: flex;
  flex-direction: column;
  margin: 1rem;
}


.hot_news_time {
  font-size: 1rem;
  justify-content: end;
  display: flex;
}

.hashtag {
  margin: .5rem auto;
  background: #eef2f5;
  cursor: pointer;
  box-shadow: 0 0 1px #eef2f5;
  border-radius: 4px;
  padding: 8px 20px;
  color: #6b7175;
}

.hashtag p {
  margin: 0rem;
}

.hashtag_layout {
  display: -webkit-inline-box;
  flex-direction: column;
  flex-wrap: wrap;

}

.cand_right {
  margin: .8rem auto;
}

@media screen and (max-width: 768px) {
  .cand_right {
    margin: auto;
    margin-top: -1rem;
  }
}
</style> 