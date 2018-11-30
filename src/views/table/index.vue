<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row>
      <el-table-column align="center" label="ID" width="95">
        <template slot-scope="scope">
          {{ scope.row.id }}
        </template>
      </el-table-column>
      <el-table-column label="Title">
        <template slot-scope="scope">
          <el-input v-if="scope.row.edit" v-model="scope.row.titleNew" />
          <span v-if="!scope.row.edit" @click="handleClickEdit(scope.row)">{{ scope.row.title }}</span>
        </template>
      </el-table-column>
      <el-table-column label="Author" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="Pageviews" width="110" align="center">
        <template slot-scope="scope">
          {{ scope.row.pageviews }}
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="Status" width="110" align="center">
        <template slot-scope="scope">
          <el-tag :type="scope.row.status | statusFilter">{{ scope.row.status }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="created_at" label="Display_time" width="200">
        <template slot-scope="scope">
          <i class="el-icon-time"/>
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="操作"
        width="100">
        <template slot-scope="scope">
          <el-button v-if="cancleShow && scope.row.edit" type="text" size="small" @click="handleClick(scope.row)">取消</el-button>
          <el-button v-if="!cancleShow || !scope.row.edit" type="text" size="small" @click="handleClickEdit(scope.row)">编辑</el-button>
          <el-button v-if="cancleShow && scope.row.edit" type="text" size="small" @click="handleClickSave(scope.row)">保存</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      :total="listLenght"
      :page-size="10"
      prev-text="上一页"
      next-text="下一页"
      style="margin-top: 30px;"
      align="right"
      background
      layout="prev, pager, next"
      @current-change="currentChange"/>
  </div>
</template>

<script>
import { getList } from '@/api/table'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: null,
      listLoading: true,
      cancleShow: false,
      listLenght: 0
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    setItemEditStatus(row, status, cancleStatus, isSave) {
      const list = this.list
      list.forEach((data) => {
        data.edit = false
      })
      const editItem = list.find((data) => data.id === row.id)
      editItem.edit = status
      editItem.titleNew = isSave ? editItem.titleNew : editItem.title
      this.cancleShow = cancleStatus
    },
    handleClick(row) {
      this.setItemEditStatus(row, false, false)
    },
    handleClickEdit(row) {
      this.setItemEditStatus(row, true, true)
    },
    handleClickSave(row) {
      this.setItemEditStatus(row, false, false, true)
      const editItem = this.list.find((data) => data.id === row.id)
      editItem.title = editItem.titleNew
    },
    fetchData(page = 1) {
      this.listLoading = true
      getList({ page }).then(response => {
        this.list = response.data.items
        this.listLenght = response.data.total
        this.list.forEach((data) => {
          data.titleNew = data.title
        })
        this.listLoading = false
      })
    },
    currentChange(e) {
      this.fetchData(e)
    }
  }
}
</script>
