<template>
  <div class="lumos-tabbar is-fixed">
    <template v-for="(tab) in this.atabs">
      <router-link class="tabbar-item" :key="tab.name" :to="tab.pagePath">
        <div class="tabbar-item-icon">
          <img v-if="!tab.selected" :src="tab.iconPath">
          <img v-if="tab.selected" :src="tab.selectedIconPath">
        </div>
        <div class="tabbar-item-text">
          <span :class="tab.selected?'active':'normal'" >{{ tab.text }}</span>
        </div>
        <div class="tabbar-item-vonbadge">
          <span :class="tab.vonBadge.type">{{ tab.vonBadge.text }}</span>
        </div>
      </router-link>
    </template>
  </div>
</template>
 
<style>
.lumos-tabbar {
  bottom: 0;
  left: 0;
  width: 100%;
  height: 3.4rem;
  z-index: 10;
  background-color: #fff;
  flex-wrap: wrap;
  margin: 0;
  padding: 0;
  display: flex;
  border-top: 1px solid #f8f8f8;
}
.lumos-tabbar.is-fixed {
  position: fixed;
}
.lumos-tabbar .tabbar-item {
  display: flex;
  flex: 1;
  flex-direction: column;
  position: relative;
  text-decoration: none;
}

.lumos-tabbar .tabbar-item-icon {
  flex: none;
  height: 1.2rem;
  width: 1.2rem;
  text-align: center;
  margin: auto;
}

.lumos-tabbar .tabbar-item-icon img {
  display: block;
  width: 100%;
  height: 100%;
}

.lumos-tabbar .tabbar-item-text {
     font-size: .8rem;
    line-height: 1.2rem;
}

.lumos-tabbar .tabbar-item-text .active {
  color: #006dee;
}

.lumos-tabbar .tabbar-item-text .normal {
  color: #7d7e80;
}

.lumos-tabbar .tabbar-item-vonbadge {
  position: absolute;
  top: 2px;
  left: 50%;
  margin-left: 6px;
  
}

</style>

<script>
export default {
  name: "lumos-tabbar",
  data() {
    return {
      atabs: this.tabs
    };
  },
  props: {
    tabs: Array
  },
  methods: {
    setVonbadgeText(index, text) {
      this.atabs[index].vonBadge.text = text;
    },
    setTab() {
      var m_cur_route_name = this.$route.name;

      for (var i = 0; i < this.atabs.length; i++) {
        var l_name = this.atabs[i].name;

        this.atabs[i].selected = false;

        if (l_name == m_cur_route_name) {
          this.atabs[i].selected = true;
        }
      }

      //var m_cur_route_name = this.$route.name;
      console.log("改变路由:" + m_cur_route_name);
      //this.selected = sessionStorage.getItem('pageUrl')
    }
  },
  mounted: function() {
    this.setTab();
  },
  watch: {
    $route() {
      this.setTab();
    }
  }
};
</script>

