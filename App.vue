<template>
  <div>
    <!-- 显示 -->
    <div class="show">0{{ showFirstLeft }}0{{ showFirstRight }}</div>
    <!-- 计数 -->
    <table>
      <tr>
        <td><button>-</button></td>
        <td><button @click="leftFirst === 0 ? 0 : leftFirst--">-</button></td>
        <td><button>-</button></td>
        <td><button>-</button></td>
        <td><button @click="rightFirst === 0 ? 0 : rightFirst--">-</button></td>
        <td><button>-</button></td>
      </tr>
      <tr>
        <td>0</td>
        <td>{{ leftFirst }}</td>
        <td>s</td>
        <td>0</td>
        <td>{{ rightFirst }}</td>
        <td>s</td>
      </tr>
      <tr>
        <td><button>+</button></td>
        <td><button @click="leftFirst++">+</button></td>
        <td><button>+</button></td>
        <td><button>+</button></td>
        <td><button @click="rightFirst++">+</button></td>
        <td><button>+</button></td>
      </tr>
    </table>
    <!-- 控制 -->
    <button class="start" @click="begin">开始</button>
    <button class="start" @click="end">结束</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //显示
      showFirstRight: 0,
      showFirstLeft: 0,
      //计数
      leftFirst: 0,
      rightFirst: 0,
      //定时器
      timer: null,
    };
  },

  methods: {
    begin() {
      // 控制变换左右
      var flag = true;
      this.timer = setInterval(() => {
        // flag为真走右边  flag为假走右边
        if (flag) {
          if (this.showFirstRight < this.rightFirst) {
            this.showFirstRight++;
          }
          if (this.showFirstRight === this.rightFirst) {
            this.showFirstRight = 0;
            flag = false;
            console.log("变了", flag);
          }
        } else {
          if (this.showFirstLeft < this.leftFirst) {
            this.showFirstLeft++;
          }
          if (this.showFirstLeft === this.leftFirst) {
            this.showFirstLeft = 0;
            flag = true;
          }
        }
      }, 1000);
    },
    end() {
      // 清除定时器
      clearInterval(this.timer);
      // 重置
      this.showFirstRight = 0;
      this.showFirstLeft = 0;
      this.leftFirst = 0;
      this.rightFirst = 0;
    },
  },
};
</script>

<style>
table {
  text-align: center;
}
button {
  width: 25px;
  height: 25px;
  margin-right: 4px;
}
.show {
  font-size: 20px;
}
.start {
  margin-top: 10px;
  width: 50px;
}
</style>