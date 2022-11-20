<template>
  <section class="canvas_page_container">
    <div class="header_box">
      <div class="header">
        <img src="../assets/images/logo/logo-group.png" alt="" />
      </div>
    </div>
    <div class="canvas_wrapper">
      <div class="canvas_switch_btn_group">
        <button id="signBtn" class="switch_sign_btn" @click="isSign">{{ sign_text }}</button>
        <button id="uploadBtn" class="switch_upload_btn" @click="switchToUpload">{{ upload_text }}</button>
      </div>
      <div class="canvas_group_wrapper">
        <!-- 手寫簽名 -->
        <div class="canvas_group own_signature" v-show="isSignBoard">
          <div class="colors_box">
            <ul class="color_options" v-show="colorOptions">
              <li class="color selected"></li>
              <li class="color"></li>
              <li class="color"></li>
            </ul>
          </div>
          <div class="canvas_box">
            <canvas id="canvas_board"  width="500"
      height="300"></canvas>
          </div>
        </div>
        <!-- 匯入簽名 -->
        <div class="canvas_group img_signature" v-show="isUploadFile">
          <div class="canvas_box">
            <label for="select_sign_img" class="label_upload_signature_img"
              >+ 請選擇檔案</label
            >
            <input
              type="file"
              accept="image/*"
              id="select_sign_img"
              name="image"
              class="input_upload_signature"
            />
            <canvas id="canvas_board"></canvas>
          </div>
        </div>
        <div class="canvas_main_btn_group">
          <button class="clear_btn">{{ clear_text }}</button>
          <button class="create_btn main_btn">{{ create_text }}</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { removeProperties } from '@babel/types';

export default {
  data() {
    return {
      sign_text: "手寫簽名",
      upload_text: "匯入簽名檔",
      clear_text: "清除",
      create_text: "建立簽名",
      isUploadFile: false,
      colorOptions: true,
      isSignBoard: true,
    };
  },
  methods:{
    isSign(){
        this.isSignBoard = true;
        this.isUploadFile = false;
        this.colorOptions = true;
        const signBtn = document.querySelector("#signBtn").classList;
        signBtn.add('switch_sign_btn');
        const uploadBtn = document.querySelector("#uploadBtn").classList;
        uploadBtn.add('switch_upload_btn');
        uploadBtn.remove('switch_sign_btn');
    },
    switchToUpload(){
        this.colorOptions = false;
        this.isSignBoard = false;
        this.isUploadFile = true;
        const uploadBtn = document.querySelector("#uploadBtn").classList;
        uploadBtn.add('switch_sign_btn');
        const signBtn = document.querySelector("#signBtn").classList;
        signBtn.remove('switch_sign_btn');
        signBtn.add('switch_upload_btn');
    }
  },
  mounted() {
    const canvas = document.querySelector("#canvas_board");
    const ctx = canvas.getContext("2d");
    const clearCanvas = document.querySelector(".clear_btn");
    const colorBtns = document.querySelectorAll(".color");

    let prevMouseX, prevMouseY, snapshot,
    isDrawing = false,
    selectedTool = "brush",
    brushWidth = 5,
    selectedColor = "#000";

    window.addEventListener("load", () => {
      canvas.width = canvas.offsetWidth;
      canvas.height = canvas.offsetHeight;
    });

    const startDraw = (e) => {
      isDrawing = true;
      ctx.beginPath(); //createing new path to draw
      ctx.strokeStyle = selectedColor;
      ctx.fillStyle = selectedColor;
    };
    const drawing = (e) => {
      if (!isDrawing) return;
      ctx.lineTo(e.offsetX, e.offsetY);
      ctx.stroke();
    };
    //顏色選取事件效果
    colorBtns.forEach((btn) => {
      btn.addEventListener("click", () => {
        document
          .querySelector(".color_options .selected")
          .classList.remove("selected");
        btn.classList.add("selected");
        //更換選取 background-color 的顏色
        selectedColor = window
          .getComputedStyle(btn)
          .getPropertyValue("background-color");
      });
    });
    //清除整個canvas
    clearCanvas.addEventListener("click", () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    });

    canvas.addEventListener("mousedown", startDraw);
    canvas.addEventListener("mousemove", drawing);
    canvas.addEventListener("mouseup", () => (isDrawing = false));
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/base/style.scss";
@import "../assets/scss/canvas.scss";
</style>
