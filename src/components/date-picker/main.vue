<template>
  <div class="lemon-date-picker">
    <input type="text" v-model="dateStr" @focus="show">
    <div class="calendar" v-if="visable">
      <table>
        <thead>
          <tr>
            <th v-for="(name, index) in dayNames" :key="index">
              {{ name }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in details" :key="index">
            <td v-for="(item2, n2) in item" :key="n2" @click="selectDate(item2.moment)">
              {{ item2.date }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import './main.scss';
export default {
  data() {
    return {
      dateStr: '',
      visable: false,
      dayNames: ['日', '一', '二', '三', '四', '五', '六'],
      details: []
    }
  },
  methods: {
    show() {
      this.visable = true;
      this.details = this.getDetails();
    },
    hide() {
      this.visable = false;
    },

    // 获取详情
    getDetails() {
      const date = moment();
      date.date(1);

      // console.log(date.date());
      // 开始的星期位置
      let start = date.day();
      date.add(-start, 'day');

      const details = [];
      // 纵向
      for (let i = 0; i < 6; i++) {
        let item = [];

        details.push(item);

        // 横向
        for (let j = 0; j < 7; j++) {
          item.push({
            date: date.date(),
            moment: moment(date)
          });
          date.add(1, 'day');
        }
      }

      return details;
    },

    // 选择日期
    selectDate(date) {
      this.dateStr = date.format('YYYY-MM-DD');
      this.hide();
    }
  }
}
</script>
