<template>
  <div>
    <el-button
      @click="dialogVisible = true"
      type="text"
      size="small"
      v-if="true"
      >获取二维码</el-button
    >
    <el-dialog :visible.sync="dialogVisible" width="30%" class="m_dialog_new" >
      <img :src="qrcode" style="width: 290px" alt="" srcset="" v-loading="loading" />
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="downloadImage(qrcode, 'a')"
          >下载</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>

<script>
// import Clipboard from "clipboard";
export default {
  data() {
    return {
      dialogVisible: false,
      qrcode:
        "https://static.rongxintech.cn/oryx/4aa368da4113e04a570d/20220225/16457740141017394.png",
    };
  },
  props: {},
  methods: {
    downloadImage(imgsrc, name, cb) {
      let image = new Image();
      // 解决跨域 Canvas 污染问题
      image.setAttribute("crossOrigin", "anonymous");
      image.onload = function () {
        let canvas = document.createElement("canvas");
        canvas.width = image.width;
        canvas.height = image.height;
        let context = canvas.getContext("2d");
        context.drawImage(image, 0, 0, image.width, image.height);
        let url = canvas.toDataURL("image/png"); // 得到图片的base64编码数据
        let a = document.createElement("a"); // 生成一个a元素
        let event = new MouseEvent("click"); // 创建一个单击事件
        a.download = name || "photo"; // 设置图片名称
        a.href = url; // 将生成的URL设置为a.href属性
        a.dispatchEvent(event); // 触发a的单击事件
        cb && cb();
      };
      image.src = imgsrc;
    },
    // getQRCode() {
    //   console.log("getQRCode....");
    //   const qrcode =
    //     "https://static.rongxintech.cn/oryx/4aa368da4113e04a570d/20220225/16457740141017394.png";
    //   this.$alert(
    //     ` <img src=${qrcode} style="width:300px;height: 280px;">
    //                 <a class='download' :href=${qrcode}' download=""  title="下载">下载</a>
    //                  `,
    //     {
    //       dangerouslyUseHTMLString: true,
    //     }
    //   );
    // },
  },
};
</script>



<style lang="scss" scoped>
.code-content {
  padding: 10px 10px 35px 10px;
}
.code-image {
  padding-right: 60px;
  border-right: 1px solid #e4e7ed;
  img {
    width: 220px;
    height: 220px;
  }
}

.el-input {
  margin-right: 10px;
  width: 320px;
}

.el-button {
  padding: 11px 13px;
}

.el-link {
  margin-top: 20px;
}

.code-path-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  flex: 1;
  margin-left: 20px;
}

.code-path {
  display: flex;
  margin-top: 10px;
}

.code-text {
  margin-top: 20px;

  &:first-child {
    margin-top: 0;
  }

  &:last-child {
    cursor: pointer;
  }
}
</style>
