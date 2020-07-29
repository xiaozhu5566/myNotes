## 页面重新加载一次
场景：大概是这样的，做了一个可以动态改变表单的页面。现在点击”重置“（reset）按钮，希望表单连同数据一起重置到最初始的状态。
（最初始时，页面可能是有数据的，不一定表单都是空的）
我思考了一下，最初是的状态就是第一次进入页面的状态。于是想着页面再次加载一次就好了（数据也回到了最初的状态）。[参考链接](https://blog.csdn.net/weixin_42383575/article/details/88660976)

解决：通过<router-view>、[provide、inject](https://cn.vuejs.org/v2/guide/components-edge-cases.html#%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5) 实现

```javascript
<router-view v-if="isRouterAlive"></router-view>
export default {
  name: "xxx",
  components: {
    bigmacEntry
  },
  data () {
    return {
      isRouterAlive: true
    }
  },
  provide () {
    return {
      reload: this.reload
    }
  },
  methods: {
    reload () {
      this.isRouterAlive = false;
      this.$nextTick(function () {
        this.isRouterAlive = true;
      })
    }
  }
};
```

```javascript
<scipt>
export default {
  inject: ['reload'],
  method: {
    reset () {
      this.reload();
    }
  }
}
<script>
```