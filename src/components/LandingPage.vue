<template>
  <section class="landing_section">
    <div class="landing_wrapper">
      <div class="header_box">
        <div class="header">
          <img src="../assets/images/logo/logo-group.png" alt="" />
          <button class="record_btn">歷史記錄</button>
        </div>
      </div>
      <div class="banner_intro">
        <div class="banner_intro_wrapper">
            <span class="dec_btn">免費試用版</span>
        <div class="banner_title_box">
          <h1>{{ mainTitle }}</h1>
          <p class="title_main_text">
            {{ mainText }}
          </p>
        </div>
        <div class="banner_content">
          <img src="../assets/images/landing/files.png" alt="" class="file_img">
          <form class="file_upload_box">
            <label class="main_upload_label main_btn" for="upload_file"
              >選擇檔案</label
            >
            <input
              id="upload_file"
              class="upload_file_input"
              type="file"
              accept=".pdf, .jpg"
              onchange="checkFileSize()"
              @change="jump"
            />
            <div class="content_text">
              <!-- <p class="text_style_draggable">或拖移檔案到此處</p> -->
              <span class="text_style_limit" id="error">(限10MB 內的PDF或JPG檔)</span>
            </div>
          </form>
          <img src="../assets/images/landing/banner-group.png" alt="" class="banner_group_img">
          <img src="../assets/images/landing/rwd_people_group.png" alt="" class="rwd_people_group_img">
        </div>
      </div>
        </div>
    </div>
  </section>
  <Footer />
</template>

<script>
import Footer from '@/components/Footer.vue';
export default {
  components: {
    Footer,
  },
  data() {
    return {
      mainTitle: "小綠簽",
      mainText:
        "護樹、永續、減碳的綠色生活響應環保無紙化電子簽署，省時便利又環保。",
    };
  },
  methods: {
    jump () {
      this.$router.push('/About');
    }
  },
  mounted(){
    function checkFileSize() {
    const file = document.getElementById("upload_file").files[0];
    if (file.size > 10485760) {
      document.getElementById("error").innerHTML = "限10MB 內的PDF或JPG檔";
    }
  }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/base/style.scss";
@import "../assets/scss/landing.scss";
</style>