<template>
    <div>
        <h1>lista de problemas</h1>
        <el-button type="success" @click="getIssues()">Obtener emisión</el-button>
        <el-row :gutter="12">
        <!-- Código 1. -->
        <el-col :span="12" v-for="( issue, index ) in issues" :key="issue.id">
            <el-card class="box-card" shadow="hover" style="margin: 5px 0;">
            <el-row :gutter="12">
                <!-- Código 2. -->
                <el-col :span="21">{{ issue.title }}</el-col>
                <el-col :span="3">
                <el-button @click="closeIssue(index)" type="success" icon="el-icon-check" circle></el-button>            
                </el-col>
            </el-row>
            </el-card>
        </el-col>
        </el-row>
    </div>
</template>
  
<script>
import axios from 'axios';

export default {
  data() {
    return {
      issues: []
    };
  },
  methods: {
    getIssues() {
      axios.get('https://api.github.com/repos/diveintocode-corp/vue_seriese_api/issues', {
        headers: {
          'Accept': 'application/vnd.github.v3+json',
          'Content-Type': 'application/json',
        },
      })
      .then((res) => {
        this.issues = res.data;
      })
      .catch((error) => {
        console.error('Error fetching issues:', error);
      });
    },
    removeIssue(issue) {
      const index = this.issues.indexOf(issue);
      if (index !== -1) {
        this.issues.splice(index, 1);
      }
    }
  }
};
</script>

<style scoped>
.issue-card {
  margin-bottom: 10px;
}

.issue-content {
  font-weight: bold;
}
</style>