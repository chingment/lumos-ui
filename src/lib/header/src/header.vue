<template>
  <div class="lumos-header">
       <div class="button-left">
          <div class="button-icon">
            <img />
          </div>
          <div class="button-text">
            <span></span>
          </div>
       </div>
       <div class="title">
          <div class="title-text">
            <span>{{ atitle.text }}</span>
          </div>
       </div>
       <div class="button-right">
  
           <span class="button-icon"  v-show="arightButton.iconPath!=''">
           <img  :src="arightButton.iconPath"  />

           <div class="button-vonbadge">
            <span :class="arightButton.vonBadge.type" >{{ arightButton.vonBadge.text }}</span>
           </div>
         </span>
          <span class="button-text" v-show="arightButton.iconPath!=''">{{ arightButton.text }}</span>
      
       </div>
  </div>
</template>
 
<style>
.lumos-header {
  background: #006dee;
  height: 2.4rem;
  color: #fff;
  display: flex;
  align-items: center;
}

.lumos-header .button-left,
.lumos-header .button-right {
  -webkit-box-flex: 0.5;
  -ms-flex: 0.5;
  flex: 0.5;
  display: flex;
  align-items: center;
  position: relative;
}

.lumos-header > .title {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: inherit;
  font-weight: 400;
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

.lumos-header .button-left {
  justify-content: flex-start;
  padding-left: 10px;
}
.lumos-header .button-right {
  justify-content: flex-end;
  padding-right: 10px;
}

.lumos-header .button-right .button-icon {
  position: relative;
}

.lumos-header .button-right .button-icon img {
  width: 1.2rem;
  height: 1.2rem;
}

.lumos-header .button-right .button-icon .button-vonbadge {
  position: absolute;
  display: inline-block;
  padding: 2px 3px;
  z-index: 12;
  border-radius: 15px;
  background-color: #ea5a49;
  text-align: center;
  position: absolute;
  top: -6px;
  left: 50%;
  font-size: 0.1rem;
}

.lumos-header .button-right .button-text {
  margin-left: 0.3rem;
}
</style>

<script>
export default {
  name: "lumos-header",
  data() {
    return {
      atitle: this.title,
      arightButton: this.rightButton
    };
  },
  props: {
    title: {
      type: Object,
      default: ""
    },
    rightButton: {
      type: Object,
      default: {
        iconPath: "",
        text: "按钮",
        vonBadge: {
          type: "",
          text: "10"
        }
      }
    }
  },
  watch: {
    "arightButton.vonBadge.text": {
      handler(newVal, oldVal) {
        console.log(
          "header.arightButton.vonBadge.text is change:" +
            oldVal +
            "->" +
            newVal
        );
        this.$emit("rightButtonVonBadgeChange");
      },
      deep: true,
      immediate: true
    }
  }
};
</script>
