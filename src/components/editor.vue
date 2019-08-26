<template>
<div>
  <editor id="tinymce" :init="editorInit" v-model="value" @onClick="onClick"></editor>
  <!-- <p @click="edit">提交</p> -->

</div>
</template>
<script>
import tinymce from "tinymce/tinymce";
import "tinymce/themes/silver/theme";
import Editor from "@tinymce/tinymce-vue";
import "tinymce/plugins/paste"; //这个到最下面那个为需要使用的工具栏模块
import "tinymce/plugins/link";
import "tinymce/plugins/lists";
import "tinymce/plugins/image";
import "tinymce/plugins/contextmenu";
import "tinymce/plugins/wordcount";
import "tinymce/plugins/colorpicker";
import "tinymce/plugins/textcolor";
import "tinymce/plugins/media";
export default {
  components: { Editor },
  props: {
    content: {
      type: String,
      default: ""
    }
  },
  data: function() {
    return {
      name: "Editor",
      value: this.content,
      editorInit: {
        selector: "#tinymce", // DOM选择器
        language_url: "/static/tinymce/zh_CN.js", // 导入语言文件
        language: "zh_CN", //语言设置
        skin_url: "/static/tinymce/skins/lightgray", // 主题样式
        height: 500,
        browser_spellcheck: true, // 拼写检查
        branding: false, //去水印
        paste_data_images: true, // 允许粘贴图像
        // menubar: false, //隐藏最上方menu菜单
        // toolbar: false, //禁用工具栏
        // statusbar: false, // 隐藏编辑器底部的状态栏
        // elementpath:false, // 禁用下角的当前标签路径
        // setup: function(editor) {
        //   //设置自定义功能的按钮
        //   editor.addButton("uploadimg", {
        //     //单个按钮，此处的uploading是该按钮的名称
        //     icon: "http://img4.imgtn.bdimg.com/it/u=1688026885,2773767715&fm=26&gp=0.jpg", //显示的图像
        //     tooltip: "上传图片", //鼠标放上去后现在是内容
        //     onclick: function() {}
        //   });
        //   editor.addButton("geshi", {
        //     //按钮列表，此处的geshi是该按钮的名称
        //     text: "格式", //显示的文字
        //     type: "menubutton",
        //     menu: [
        //       {
        //         text: "标签",
        //         onclick: function() {}
        //       }
        //     ]
        //   });
        // },
        plugins: "link lists image code table wordcount code paste",
        toolbar:
          "bold italic underline strikethrough | fontsizeselect | forecolor backcolor | alignleft aligncenter alignright alignjustify | bullist numlist | outdent indent blockquote | undo redo | link unlink image code | removeformat"
      },
      tinymceId: null
    };
  },
  mounted() {
    console.log(this.value)
    tinymce.init({
      selector: "textarea" // change this value according to your HTML
      //启用菜单栏并显示如下项 [文件 编辑 插入 格式 表格]
      //   menubar: false,
      // 配置每个菜单栏的子菜单项（如下是默认配置）
      //   menu: {
      //     file: { title: "File", items: "newdocument" },
      //     edit: {
      //       title: "Edit",
      //       items: "undo redo | cut copy paste pastetext | selectall"
      //     },
      //     insert: { title: "Insert", items: "link media | template hr" },
      //     view: { title: "View", items: "visualaid" },
      //     format: {
      //       title: "Format",
      //       items:
      //         "bold italic underline strikethrough superscript subscript | formats | removeformat"
      //     },
      //     table: {
      //       title: "Table",
      //       items: "inserttable tableprops deletetable | cell row column"
      //     },
      //     image: { title: "image", items: "image" }
      //   }
    });
  },
  methods: {
    onClick(e) {
      console.log(this.value)
      this.$emit('onClick', e, tinymce);
    },
    handleImgUpload(blobInfo, success, failure) {
      let formdata = new FormData();
      formdata.set("upload_file", blobInfo.blob());
      axios
        .post("/api/upload", formdata)
        .then(res => {
          success(res.data.data.src);
        })
        .catch(res => {
          failure("error");
        });
    }
  },
  watch: {
    content(newValue) {
      this.value = newValue
    },
    value(newValue) {
      this.$emit('input', newValue)
    }
  }
};
</script>