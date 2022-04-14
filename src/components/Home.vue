<template>
  <div class="container">
    <el-header>
      <i class="el-icon-s-home"></i>
    </el-header>
    <el-container>
      <el-aside width="250px">
        <el-row class="tac">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose">
            <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>导航一</span>
              </template>
              <el-menu-item-group>
                <template slot="title">分组一</template>
                <el-menu-item index="1-1">选项1</el-menu-item>
                <el-menu-item index="1-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="1-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="1-4">
                <template slot="title">选项4</template>
                <el-menu-item index="1-4-1">选项1</el-menu-item>
              </el-submenu>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>导航二</span>
              </template>
              <el-menu-item-group>
                <template slot="title">分组一</template>
                <el-menu-item index="2-1">选项1</el-menu-item>
                <el-menu-item index="2-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="2-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="2-4">
                <template slot="title">选项4</template>
                <el-menu-item index="2-4-1">选项1</el-menu-item>
              </el-submenu>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>导航一</span>
              </template>
              <el-menu-item-group>
                <template slot="title">分组一</template>
                <el-menu-item index="3-1">选项1</el-menu-item>
                <el-menu-item index="3-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="3-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="3-4">
                <template slot="title">选项4</template>
                <el-menu-item index="3-4-1">选项1</el-menu-item>
              </el-submenu>
            </el-submenu>
          </el-menu>
        </el-row>
      </el-aside>
      <el-main>
        <el-tabs v-model="editableTabsValue" type="card" editable @edit="handleTabsEdit">
          <el-tab-pane
            :key="item.name"
            v-for="(item) in editableTabs"
            :label="item.title"
            :name="item.name">
            {{item.content}}
            <!--                  <router-view></router-view>-->
          </el-tab-pane>
        </el-tabs>
      </el-main>
    </el-container>
    <el-footer></el-footer>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      editableTabsValue: '2',
      editableTabs: [{
        title: 'Tab 1',
        name: '1',
        content: 'Tab 1 content'
      }, {
        title: 'Tab 2',
        name: '2',
        content: 'Tab 2 content'
      }],
      tabIndex: 2
    }
  },
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    },
    handleTabsEdit (targetName, action) {
      // if (action === 'add') {
      //   let newTabName = ++this.tabIndex + ''
      //   this.editableTabs.push({
      //     title: 'New Tab',
      //     name: newTabName,
      //     content: 'New Tab content'
      //   })
      //   this.editableTabsValue = newTabName
      // }
      if (action === 'remove') {
        let tabs = this.editableTabs
        let activeName = this.editableTabsValue
        if (activeName === targetName) {
          tabs.forEach((tab, index) => {
            if (tab.name === targetName) {
              let nextTab = tabs[index + 1] || tabs[index - 1]
              if (nextTab) {
                activeName = nextTab.name
              }
            }
          })
        }
        this.editableTabsValue = activeName
        this.editableTabs = tabs.filter(tab => tab.name !== targetName)
      }
    },
    changeTheme: function (value) {
      let eleLinks = document.querySelectorAll('link[title]')
      this.colorChange(eleLinks, value)
    },
    colorChange: function (eleLinks, value) {
      eleLinks.forEach(function (link) {
        link.disabled = true
        if (link.getAttribute('title') === value) {
          link.disabled = false
        }
      })
    }
  }
}
</script>

<style scoped lang="less">
.container {
  height: 100vh;// 页面高度
  display: flex;
  flex-wrap: wrap;// 自动换行
  flex-direction: column;// 容器属性 垂直方向
  .el-header /deep/ {
    border: black solid 1px;
    background-color: #dcaf94;
    height: 100px;
    width: 100%;
    .el-icon-s-home {
      font-size: 2em;
      margin-top: 10px;
      margin-left: 20px;
    }
  }
  .el-container {
    border: red solid 1px;
    padding: 0 50px;
    background-color: #fcede4;
    overflow: auto;
    flex: 1;
    .el-aside {
      border: black solid 1px;
      .el-row {
        width: 200px;
        /deep/ .el-menu {
          border-right: none;
          //height: 0;
          background-color: transparent;
        }
      }
    }
    .el-main {
      border: black solid 1px;
      .el-tabs {
        .el-icon-plus{
          display: none;
        }
      }
    }
  }
  .el-footer {
    border: black solid 1px;
    width: 100%;
    background-color: #f9a7a7;
    height: 100px;
    margin-bottom: 0;
  }
}

</style>
