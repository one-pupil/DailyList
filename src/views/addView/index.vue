<template>
  <div class="add-wrapper">
    <div class="content">
      <mu-text-field hintText="输入你的目标" v-model="addData.goal" :required="true" :underlineShow="false" @blur="check(addData.goal)"/><br/>
      <mu-text-field hintText="一些激励的话" v-model="addData.snippet" :required="true" :underlineShow="false" @blur="check(addData.snippet)"/><br/>
      <mu-date-picker hintText="计划坚持日期" v-model="addData.targetDate"/> <br/>
      <mu-raised-button label="保存" class="demo-raised-button" secondary @click="addSave()"/>
    </div>
  </div>
</template>
<style lang="less" rel="stylesheet/less" scope>
  .add-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    .mu-text-field-input {
      border-bottom: 1px solid rgba(0, 0, 0, 0.12);
    }
    .mu-text-field-line {
      height: 0;
    }
    .demo-raised-button {
      margin-left: 85px;
    }
  }
</style>
<script type='text/ecmascript-6'>
  import { addList } from 'api/list';
  export default {
    data() {
      return {
        addData: {
          goal: '',
          snippet: '',
          targetDate: '',
          ownerId: '',
          isDone: false,
          details: {
            isToday: false,
            startDay: null,
            yesterday: null,
            totalDays: [],
            sumTotal: 0
          }
        }
      }
    },
    created() {
      this.addData.ownerId = this.$store.getters.userInfo.objectId;
    },
    methods: {
      check(val) {

      },
      addSave() {
        addList(this.addData).then((res) => {
          if (res.status === 201) {
            this.$router.push({path: '/index'});
          }
        });
      }
    }
  }
</script>
