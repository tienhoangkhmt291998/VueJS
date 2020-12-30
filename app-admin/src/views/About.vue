<template>
  <div>
    <el-table
    :data="handleSearch"
    style="width: 100%">
    <el-table-column
      label="Id"
      prop="id">

    </el-table-column>
    <el-table-column
      label="Title"
      prop="title">
    </el-table-column>
    <el-table-column
      align="right"
      >
      <template slot="header" slot-scope="{}">
          <el-input
          v-model="search"
          size="mini"
          placeholder="search"
          />
      </template>
      <template  slot-scope="{}">
        
      </template>
    </el-table-column>
    <el-table-column>
      <template slot="header" slot-scope="{}" >
         <el-button
          size="mini"
          type="primary"
          @click="newUser">New User</el-button>
          
      </template>
        <template  slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.row.id,scope.row.title)">Edit</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.row.id, scope.row.title)">Delete</el-button>
      </template>
    </el-table-column>
  </el-table>
  <pagination />
  </div>
</template>

<script>
// import axios from 'axios';
import pagination from './pagination';
export default {
  components:{ pagination },
  data() {
      return {
        arr:this.$store.state.arr,
        search: this.$store.state.search,
      }
    },
    methods: {
      handleEdit(index, title) {
        this.$store.state.title = title
        this.$router.push(`/User/${index}/edit`)
      },
      newUser() {
        this.$router.push("/User/New")
        this.$store.state.btn_new = false
      },
      handleDelete(index, title) {

        this.$confirm(title, 'Cảnh Cáo', {

          confirmButtonText: 'OK',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          let id = this.$store.state.arr;

          for (let i = 0; i < id.length; i++) {

            if (id[i].id === index){
              id.splice(i, 1)
            }
          }

          this.$message({
            type: 'success',
            message: 'Xóa Thành Công',
          });

        }).catch(() => {
          this.$message({
            type: 'info',
            message: 'Đã Hủy Xóa'
          });
        });
      },

    },
    mounted () {
      this.$store.state.btn_new = true;
    },
    computed:{
       handleSearch () {
         if (!this.search) {
           return this.$store.state.arr.slice(this.$store.state.index, this.$store.state.currentIndex)
         }
        return this.$store.state.arr.filter(
            (data) => {
              if(this.search) {
                return data.title.toLowerCase().includes(this.search.toLowerCase())
              }else{
                let data_search = data.slice(10,20)
                return data_search;
              }
            }
        )
      },
    }
  }

</script>