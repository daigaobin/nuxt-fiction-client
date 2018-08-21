<template>
  <section class="container">
    <div class="search">
      <el-input placeholder="请输入书名" v-model="searchWord">
        <template slot="append">
          <el-button slot="append" icon="el-icon-search"></el-button>
        </template>
      </el-input>
    </div>
    <div class="content">
      <h3>最热</h3>
      <el-table :data="tableData"
                border
                stripe
                style="width: 100%">
        <el-table-column prop="bookName"
                         label="书名"
                         align="center">
        </el-table-column>
        <el-table-column prop="author"
                         label="作者"
                         align="center">
        </el-table-column>
        <el-table-column prop="latestChapter"
                         label="最新章节"
                         align="center">
        </el-table-column>
        <el-table-column prop="source"
                         label="来源"
                         align="center">
        </el-table-column>
        <el-table-column prop="updateTime"
                         label="更新时间"
                         align="center">
        </el-table-column>
      </el-table>

      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="pageSizes"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
        class="f-r">
      </el-pagination>
    </div>
  </section>
</template>

<script>
  import axios from 'axios';

  export default {
    components: {},
    data() {
      return {
        searchWord: '',
        tableData: [],
        currentPage: 1,
        total: 0,
        pageSize: 20,
        pageSizes: [20, 40, 80, 100]
      }
    },
    created() {
      this.init();
    },
    mounted() {

    },
    methods: {
      init() {
        this.getHotFictionList();
      },
      getHotFictionList() {
        axios.get('/api/getHotFictionList').then(resp => {
          if (resp && resp.status === 200) {
            this.tableData = resp.data;
            debugger
          }
        });
      },
      handleSizeChange() {

      },
      handleCurrentChange() {

      }
    }
  }
</script>

<style scoped lang="scss">
  .container {
    width: 80%;
    margin: 20px auto;
    .f-r {
      float: right;
    }
  }
</style>

