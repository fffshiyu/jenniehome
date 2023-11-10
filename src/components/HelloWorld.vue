<template>
  <div class="ad-img">
    <ul class="nav-left">
      <li><a href="#" alt="working on it">ME</a><span>|</span></li>
      <li><a href="#" alt="working on it">WORK</a><span>|</span></li>
      <li><a href="#" alt="working on it">JOKE</a><span>|</span></li>
      <li><a href="#" alt="working on it">ART-</a><span>|</span></li>
      <li><a href="#" alt="working on it">LIFE</a><span>|</span></li>
    </ul>
    <ul class="nav-right">
      <li><a href="https://www.instagram.com/jenniefofofo/"><img src="../assets/images/instagram.svg" alt=""></a></li>

      <li><a @click="openModal"><img src="../assets/images/wechat.svg" alt=""></a></li>

      <li><a href="https://www.youtube.com/@jenniefofo0306
"><img src="../assets/images/youtube.svg" alt=""></a></li>
      <li><a href="#"><img src="../assets/images/email-fill.svg" alt=""></a></li>
    </ul>

  </div> 

  <!-- Modal -->
  <div v-if="showModal" class="modal">
    <div class="modal-content">
      <span class="close" @click="closeModal">&times;</span>
      <img src="../assets/images/wechat.jpg" alt="WeChat QR Code">

    </div>
  </div>
  <div id="scene-container"></div>
</template>

<script>
export default {
  data() {
    return {
      showModal: false,
    };
  },

  methods: {
    openModal() {
      this.showModal = true;
      console.log('Modal opened', this.showModal);
    },

    closeModal() {
      this.showModal = false;

    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ad-img {
  width: 100%;
  height: 100px;
  background: url(../assets/images/ad.jfif) center/cover no-repeat;
  /* 合并 background 属性 */
}

.nav-left {
  display: flex;
  justify-content: center;
  align-items: center;
  float: left;
}

.nav-right {
  display: flex;
  justify-content: center;
  align-items: center;
  float: right;
  margin-right: 60px;
}

.nav-left li {
  list-style: none;
}

.nav-right li {
  list-style: none;
}

.nav-left a,
.nav-left span {
  text-decoration: none;
  color: #f4a7ba;
  font-size: 12px;
  line-height: 50px;
  padding-inline-start: 20px;
  /* font-weight: 700; 将文本加粗 */
  /* 设置行高与容器高度匹配 */
}

.nav-right a,
.nav-right span {
  text-decoration: none;
  color: #f4a7ba;
  height: 15px;
  width: 15PX;
  line-height: 50px;
  padding-inline-start: 20px;
  /* font-weight: 700; 将文本加粗 */
  /* 设置行高与容器高度匹配 */
}

.nav-left a:hover {
  color: whitesmoke;
}

.nav-left span {
  display: inline-block;
  vertical-align: middle;
  margin: 0 5px;
}

#scene-container {
  width: 100%;
  height: 100%;
  overflow: hidden;
  /* 可以添加溢出隐藏，以确保内容不会溢出容器 */
}

img {
  height: 15px;
  width: 15px;
}

.nav-right a:hover img {
  filter: brightness(100);
  /* 切换图片颜色为白色 */
}

/* Styles for the modal */
.modal {
  display: block;
  position: fixed;
  z-index: 9999;
  /* 将 z-index 设置为更高的值 */
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.75);
}


.modal-content {
  position: relative;
  background-color: #fefefe;
  margin: 15% auto;
  padding: 100px;
  max-width: 100px;
}

.close {
  position: absolute;
  top: 0;
  right: 0;
  padding: 10px;
  cursor: pointer;
}

.modal-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.modal-content img {
  width: 100%;
  height: 100%;
  /* 调整为你需要的高度 */
  margin: auto;
  /* 水平和垂直居中 */
}

body {
  max-width: 1200px;
  /* 设置适当的最大宽度 */
  margin: 0 auto;
  /* 居中对齐 */
}
</style>
