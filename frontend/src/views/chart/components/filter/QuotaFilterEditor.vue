<template>
  <el-col>
    <el-button icon="el-icon-plus" circle size="mini" style="margin-bottom: 10px;" @click="addFilter" />
    <div style="max-height: 50vh;overflow-y: auto;">
      <el-row v-for="(f,index) in item.filter" :key="index" class="filter-item">
        <el-col :span="4">
          <span>{{ item.name }} ({{ $t('chart.'+item.summary) }})</span>
        </el-col>
        <el-col :span="8">
          <el-select v-model="f.term" size="mini">
            <el-option-group
              v-for="(group,idx) in options"
              :key="idx"
              :label="group.label"
            >
              <el-option
                v-for="opt in group.options"
                :key="opt.value"
                :label="opt.label"
                :value="opt.value"
              />
            </el-option-group>
          </el-select>
        </el-col>
        <el-col :span="6">
          <el-input v-show="!f.term.includes('null')" v-model="f.value" class="value-item" :placeholder="$t('chart.condition')" size="mini" clearable />
        </el-col>
        <el-col :span="6">
          <el-button type="text" icon="el-icon-delete" circle style="float: right" @click="removeFilter(index)" />
        </el-col>
      </el-row>
    </div>
  </el-col>
</template>

<script>
export default {
  name: 'QuotaFilterEditor',
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      options: [{
        label: '',
        options: [{
          value: 'eq',
          label: this.$t('chart.filter_eq')
        }, {
          value: 'not_eq',
          label: this.$t('chart.filter_not_eq')
        }]
      },
      // {
      //   label: '',
      //   options: [{
      //     value: 'like',
      //     label: this.$t('chart.filter_like')
      //   }, {
      //     value: 'not like',
      //     label: this.$t('chart.filter_not_like')
      //   }]
      // },
      {
        label: '',
        options: [{
          value: 'lt',
          label: this.$t('chart.filter_lt')
        }, {
          value: 'gt',
          label: this.$t('chart.filter_gt')
        }]
      },
      {
        label: '',
        options: [{
          value: 'le',
          label: this.$t('chart.filter_le')
        }, {
          value: 'ge',
          label: this.$t('chart.filter_ge')
        }]
      },
      {
        label: '',
        options: [{
          value: 'null',
          label: this.$t('chart.filter_null')
        }, {
          value: 'not_null',
          label: this.$t('chart.filter_not_null')
        }]
      }]
    }
  },
  mounted() {
  },
  methods: {
    addFilter() {
      this.item.filter.push({
        term: 'eq',
        value: ''
      })
    },
    removeFilter(index) {
      this.item.filter.splice(index, 1)
    }
  }
}
</script>

<style scoped>
.filter-item{
  width: 100%;
  border-radius: 4px;
  border: 1px solid #DCDFE6;
  padding: 4px 14px;
  margin-bottom: 10px;
  display: flex;
  justify-content: left;
  align-items: center;
}
.form-item>>>.el-form-item__label{
  font-size: 12px;
}
  span{
    font-size: 12px;
  }

  .value-item>>>.el-input{
    position: relative;
    display: inline-block;
    width: 80px!important;
  }
.el-select-dropdown__item{
  padding: 0 20px;
  font-size: 12px;
}
</style>
