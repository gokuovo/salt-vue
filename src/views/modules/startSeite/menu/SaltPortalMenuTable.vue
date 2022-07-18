<template>
  <div v-loading.fullscreen.lock="loading">
    <el-button
      type="primary"
      size="mini"
      @click="add()"
    >{{ '保存' }}</el-button>
    <el-button
      icon="el-icon-search"
      size="mini"
      type="primary"
      @click="pageIndex=1;getDataList()"
    >查询</el-button>
    <div style="margin-top: 20px" />
    <el-table :data="dataList" border tooltip-effect="dark">
      <el-table-column type="index" align="center" width="100" label="序号"></el-table-column>
      <el-table-column
        prop="menuNameEn"
        label="菜单EN名"
        align="center"
      />
      <el-table-column
        prop="menuNameChi"
        label="菜单CHI名"
        :show-overflow-tooltip="true"
        align="center"
      />
      <el-table-column
        prop="menuNameJap"
        label="菜单JAP名"
        :show-overflow-tooltip="true"
        align="center"
      />
      <el-table-column
        prop="menuNameSpa"
        label="菜单SPA名"
        :show-overflow-tooltip="true"
        align="center"
      />
      <el-table-column
        prop="url"
        label="跳转网页"
        :show-overflow-tooltip="true"
        align="center"
      />
      <el-table-column
        prop="sort"
        label="排序值"
        :show-overflow-tooltip="true"
        align="center"
      />
    </el-table>
    <el-pagination
      :current-page="curPage"
      :page-sizes="[3, 10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper"
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
    />
    <!-- <accident-rate-config-add ref="addOrUpdate" v-if="addOrUpdateVisible" @refreshDataList="getDataList()" /> -->
    <ld-code-add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList()" />
  </div>
</template>

<script>
export default {
  components: {
  },
  props: ['dataForm'],
  data() {
    return {
      dataList: [],
      curPage: 1,
      pageSize: 10,
      totalPage: 0,
      dataListLoading: false,
      loading: false,
      dataListSelections: [],
      showEdit: [], // 显示编辑框
      showBtn: [],
      showBtnOrdinary: true,
      addOrUpdateVisible: false
    }
  },
  methods: {
    getDataList() {
      this.dataListLoading = true
      this.$http({
        url: this.$http.adornUrl('/agy/ldcode/list'),
        method: 'post',
        params: this.$http.adornParams({
          curPage: this.curPage,
          pageSize: this.pageSize
        }),
        data: this.$http.adornData({
          ...this.dataForm
        })
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.dataList = data.page.list
          this.totalPage = data.page.totalCount
        } else {
          this.dataList = []
          this.totalPage = 0
        }
        this.dataListLoading = false
      })
    },
    // 新增
    add() {
      this.addOrUpdateVisible = true
      this.$nextTick(() => {
        this.$refs.addOrUpdate.init()
      })
    },

    sizeChangeHandle(val) {
      this.pageSize = val
      this.curPage = 1
      this.getDataList()
    },
    // 当前页
    currentChangeHandle(val) {
      this.curPage = val
      this.getDataList()
    },
    clearPage() {
      this.curPage = 1
    },
    // 多选
    selectionChangeHandle(val) {
      console.log(val)
      this.dataListSelections = val
    }
  }
}
</script>
