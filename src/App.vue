<template>
  <el-button
    :icon="WarningFilled"
    circle
    @click="dialogVisible = true"
    type="danger"
  />

  <el-dialog v-model="dialogVisible" title="意見反饋" width="500">
    <el-form :model="form" label-position="top">
      <el-form-item label="類別" required>
        <el-select v-model="form.category" placeholder="請選擇">
          <el-option
            v-for="item in categoryList"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
      </el-form-item>

      <el-form-item label="標題" required>
        <el-input v-model="form.title" placeholder="請輸入標題" />
      </el-form-item>

      <el-form-item label="描述" required>
        <el-input v-model="form.describe" placeholder="請描述您的意見/問題" />
      </el-form-item>

      <el-form-item label="參考圖片">
        <el-upload
          v-model:file-list="fileList"
          action="#"
          :auto-upload="false"
          list-type="picture-card"
          :limit="3"
          :on-preview="handlePictureCardPreview"
          :on-remove="handleRemove"
        >
          <el-icon><Plus /></el-icon>
        </el-upload>

        <el-dialog v-model="imageDialog">
          <img w-full :src="imageUrl" alt="Preview Image" />
        </el-dialog>
      </el-form-item>
    </el-form>
  </el-dialog>
</template>

<script setup>
import { ref, reactive } from "vue";
import { WarningFilled, Plus } from "@element-plus/icons-vue";
//import { ElMessageBox } from 'element-plus'

const dialogVisible = ref(false);
const form = reactive({});
const fileList = ref([]);

const imageDialog = ref(false);
const imageUrl = ref();

const handleRemove = (uploadFile, uploadFiles) => {
  console.log(uploadFile);
  console.log(uploadFiles);
};

const handlePictureCardPreview = (uploadFile) => {
  imageUrl.value = uploadFile.url;
  imageDialog.value = true;
};

const categoryList = [
  {
    value: 1,
    label: "操作問題",
  },
  {
    value: 2,
    label: "優化建議",
  },
  {
    value: 3,
    label: "Bug反饋",
  },
  {
    value: 4,
    label: "其他",
  },
];
</script>

<style></style>
