<template>
  <div>
    <DatePicker
      format="yyyy-MM-dd"
      :value="item.date"
      type="date"
      @on-change="updateDate"
      :options="options3"
    ></DatePicker>

    <DatePicker
      format="yyyy-MM"
      :value="item.month"
      type="month"
      @on-change="updateMonth"
      :options="options3"
    ></DatePicker>
    {{item}}
    <hr>
  </div>
</template>

<script>
import { debug } from "util";
export default {
  mounted() {
    this.item.date = this.thisDay();
    delete this.item.month;
    console.log(this.item);
  },
  methods: {
    updateDate(val) {
      this.item = { date: val };
      console.log(this.item);
    },
    //   在当前月数添加最后一天
    updateMonth(val) {
      var d = val.split("-");
      var monthEnd = new Date(d[0], d[1], 0).getDate();
      var month = val + "-" + monthEnd;
      this.item = { month: month };
      delete this.item.date;
      console.log(this.item);
    },

    lineChart() {
      console.log(this.item);
    },
    lineChart_1() {},
    PieChart() {},
    thisDay() {
      var date = new Date(); //创建时间对象
      var time =`${date.getFullYear()+"-"+(date.getMonth()+1)+"-"+(date.getDate())}`
      console.log(time);
      return time;
    }
  },
  data() {
    return {
      item: {
        date: "",
        month: ""
      },
      options3: {
        disabledDate(date) {
          return date && date.valueOf() > Date.now() - 86400000;
        }
      }
    };
  }
};
</script>

<style>
</style>
