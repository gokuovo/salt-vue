<template>
  <div>
    <el-form :inline="true" :model="dataForm" label-width="110px" :label-position="'right'">
      <el-row>
        <el-col :span="8">
          <el-form-item prop="menuEn" :label="'菜单EN名'">
            <el-input v-model="dataForm.menuNameEn" />
          </el-form-item>
        </el-col>
        <el-col :span="8">
          <el-form-item prop="menuEn" :label="'菜单CHI名'">
            <el-input v-model="dataForm.menuNameChi" />
          </el-form-item>
        </el-col>
        <el-col :span="8">
          <el-form-item prop="menuEn" :label="'菜单JAP名'">
            <el-input v-model="dataForm.menuNameJap" />
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="8">
          <el-form-item prop="menuEn" :label="'菜单SPA名'">
            <el-input v-model="dataForm.menuNameSpa" />
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
  <salt-portal-menu-table :dataForm="dataForm"></salt-portal-menu-table>
  </div>
</template>

<script>
import SaltPortalMenuTable from '@/views/modules/startSeite/menu/SaltPortalMenuTable'

export default {
  components: {
    SaltPortalMenuTable
  },
  data() {
    return {
      options: [],
      form: {},
      dataForm: {
        menuNameEn: '',
        menuNameChi:'',
        menuNameJap:'',
        menuNameSpa:'',
        wid: '100%'
      }
    }
  }
}
</script>

