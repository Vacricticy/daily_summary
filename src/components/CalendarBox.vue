<template>
  <div class="container">
    <div class="year_month">2020年11月</div>
    <div class="calendarBox">
      <div v-for="(item, index) in 30" :key="index" class="oneDay">
        <!-- 当前时间 -->
        <div class="date">11月2日</div>
        <!-- 添加任务的按钮 -->
        <a class="add" @click="addHandle($event)">+</a>
        <!-- 任务列表 -->
        <div class="jobList">
          <div
            v-for="(job, index) in oneDayjobList"
            :key="index"
            :class="['oneJob', job.state ? 'checked' : 'nochecked']"
          >
            <a class="state" @click="checkHandle($event)">{{
              job.state ? "√" : ""
            }}</a
            ><span class="content">{{ job.content }}</span>
          </div>
        </div>
        <!-- 添加任务的输入框 -->
        <div class="addJobBox" v-if="show">
          <input type="text" class="addContent" />
          <!-- 上传任务的按钮 -->
          <a class="submitBtn" @click="submitHandle($event)">↑</a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "CalenderBox",
  data() {
    return {
      oneDayjobList: [
        { content: "job1", state: true },
        { content: "job2", state: false },
        { content: "job3", state: true },
        { content: "job4", state: false },
        { content: "job4", state: false },
        { content: "job4", state: false },
        { content: "job4", state: false },
        { content: "job4", state: false },
        { content: "job9", state: false },
      ],
      addContent: "",
      show: false,
    };
  },
  methods: {
    checkHandle(e) {
      console.log(e.currentTarget.parentNode.className);
      var className = e.currentTarget.parentNode.className;
      if (className.includes("nochecked")) {
        console.log(0);
        e.currentTarget.parentNode.className = "oneJob checked";
        e.currentTarget.innerHTML = "√";
      } else {
        console.log(1);
        e.currentTarget.parentNode.className = "oneJob nochecked";
        e.currentTarget.innerHTML = "";
      }
    },
    addHandle(e) {
      // var el=e.currentTarget
      this.show = !this.show;
    },
    // 上传任务
    submitHandle(e) {
      var el = e.currentTarget.parentNode.children[0];
      console.log(el.value);
      this.oneDayjobList.unshift({
        content: el.value,
        state: false,
      });
      // console.log(this.addContent);
      this.show = false;
    },
  },
};
</script>
<style lang="less" scoped>
* {
  box-sizing: border-box;
}
.container {
  width: 100%;
  padding: 10px 0;
}
.calendarBox {
  // margin-fet: 0 auto;
  margin-left: 164px;
  width: 1501px;
  display: flex;
  flex-wrap: wrap;
  // border-top: 1px solid rgba(0, 0, 0, 0.3);
  // border-left: 1px solid rgba(0, 0, 0, 0.3);
}
.oneDay {
  position: relative;
  width: 200px;
  height: 200px;
  // border-right: 1px solid rgba(0, 0, 0, 0.3);
  // border-bottom: 1px solid rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(0, 0, 0, 0.1);
  margin: 6px;
  border-radius: 8px;
  box-shadow: 0px 0px 6px 0px rgba(0, 0, 0, 0.3);
  &:hover .add {
    // display: block;
  }
  .add {
    display: block;
    // display: none;
    position: absolute;
    top: 8px;
    right: 8px;
    width: 20px;
    height: 20px;
    text-align: center;
    line-height: 20px;
    background-color: rgb(102, 185, 102);
    border-radius: 50%;
    color: #fff;
    cursor: pointer;
    box-shadow: 2px 2px 6px 0px rgba(0, 0, 0, 0.2);
  }

  .date {
    height: 22px;
    margin: 12px 0 0 0;
    width: 100%;
    line-height: 11px;
    text-align: center;
    border-bottom: 1px solid rgba(0, 0, 0, 0.3);
  }
  .jobList {
    height: 170px;
    padding: 4px;
    font-size: 10px;
    overflow-y: scroll;
    &::-webkit-scrollbar {
      // display: none;
      width: 0 !important;
    }
    .oneJob {
      width: 100%;
      margin: 4px 6px;
      display: flex;

      .state {
        display: inline-block;
        width: 20px;
        height: 20px;
        text-align: center;
        line-height: 20px;
        border: 1px solid rgba(0, 0, 0, 0.3);
        border-radius: 5px;
        font-size: 15px;
        margin-right: 10px;
        cursor: default;
      }
    }
    .checked {
      a {
        background-color: rgb(102, 185, 102);
        color: #fff;
      }
      .content {
        text-decoration: line-through;
        color: rgba(0, 0, 0, 0.3);
      }
    }
    .nochecked a {
    }
  }
  .add:active .addJobBox {
    // display: block;
  }
  .add:active {
    transform: scale(0.8);
    box-shadow: 2px 2px 6px 2px rgba(0, 0, 0, 0.2);
  }
  .addJobBox {
    width: 100%;
    display: flex;
    align-items: center;
    position: absolute;
    top: 37px;
    padding-bottom: 2px;
    border-bottom: 1px solid rgba(0, 0, 0, 0.3);
    transition: all 2s;
    .addContent {
      width: 160px;
      height: 25px;
      border: 1px solid rgba(0, 0, 0, 0.3);
      outline: none;
      border-radius: 5px;
      margin-left: 5px;
      margin-right: 5px;
    }
    .submitBtn {
      display: inline-block;
      width: 22px;
      height: 22px;
      text-align: center;
      line-height: 22px;
      border: 1px solid rgba(0, 0, 0, 0.3);
      border-radius: 5px;
      font-size: 15px;
      // margin-right: 10px;
      cursor: default;
      background-color: rgb(68, 148, 240);
      color: #fff;
    }
    .submitBtn:active {
      transform: scale(0.9);
    }
  }
}
.year_month {
  position: fixed;
  left: 24px;
  top: 42px;
  font-size: 20px;
}
</style>
