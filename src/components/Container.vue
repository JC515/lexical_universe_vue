<template>
  <div class="common-layout">
    <el-container class="full-height">
      <el-header height="100px"
                 style="background-color: #79bbff; display: flex; justify-content: space-between; align-items: center;">
        <h1>词汇宇宙</h1>
        <Saying></Saying>
      </el-header>
      <el-container class="full-height">
        <el-aside width="200px" style="background-color: #a0cfff">
          <Menu @menuSelect="handleMenuSelect"></Menu>
        </el-aside>
        <el-main style="background-color: #d9ecff">
          <div id="page1" v-if="index === 1">
            <PersonalCenter :nowUserId="userId"></PersonalCenter>
          </div>
          <div id="page2" v-else-if="index === 2">
            <WordLearn :nowUserId="userId"></WordLearn>
          </div>
          <div id="page3" v-else-if="index === 3">
            <Quiz></Quiz>
          </div>
          <div id="page4" v-else-if="index === 4">
            <WordTable></WordTable>
          </div>
          <div v-else>
            <p>无效界面</p>
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import Menu from "@/components/SideMenu.vue";
import WordLearn from "@/components/WordLearn.vue";
import Saying from "@/components/Saying.vue";
import WordTable from "@/components/WordTable.vue";
import bus from "@/Util/EventBus";
import Quiz from "@/components/Quiz.vue";
import PersonalCenter from "@/components/PersonalCenter.vue";

export default {
  components: {
    WordTable,
    PersonalCenter,
    Menu,
    WordLearn,
    Saying,
    Quiz,
  },
  props: {
    userId: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      index: 2,
    };
  },
  methods: {
    handleMenuSelect(index) {
      index = parseInt(index, 10);
      this.index = index;
    },
  },
  watch: {
    index() {
      bus.emit("indexChange", this.index)
    },
  },
};
</script>

<style>
h1 {
  font-size: 2em;
  font-style: italic;
  color: #000000;
}

.full-height {
  height: 100%;
}

body, html {
  min-height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
}
</style>
