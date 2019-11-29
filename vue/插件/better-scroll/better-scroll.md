# better-scroll

better-scroll 是一个移动端滚动的解决方案

## 安装

``` shell
npm install --save better-scroll
```

## 基本配置

### html结构

``` shell
div.wrapper > ul.content > li
```

### css样式

```css
.wrapper {
  height: 400px;
  overflow: hidden;
}
.content {}
```

### 初始化

``` js
import Bscroll from 'better-scroll';

export default {
  data() {
    return {
     	scroll: null,
    };
  },
  mounted() {
    this.$nextTick(() => {
      if (!this.scroll) { // 获取内容之后，检测滚动对象实例化与否
        // 实例化滚动对象
        this.scroll = new Bscroll(this.$refs.wrapper, {
          // ...配置项
        });
      } else {
        // 滚动对象已存在，则刷新
        this.scroll.refresh();
      }
    });
  },
};
```

## Example

### 例子一：左侧滚动监听

``` vue
<template>
  <div id="dome">
    <h2 class="dome--title">左侧滚动监听</h2>
    <div class="dome__wrapper">
      <div class="dome__wrapper--left" ref="left">
        <ul>
          <li :class="['dome__wrapper--left--item', {'current': currentIndex == index}]"
            v-for="(item, index) in left" :key="index"
            @click="selectItem(index, $event)">{{item.name}}</li>
        </ul>
      </div>
      <div class="dome__wrapper--right" ref="right">
        <ul>
          <li class="dome__wrapper--right--item right-item-hook"
            v-for="item in right"
            :key="item.id">
            <h3>{{item.name}}</h3>
            <ul>
              <li v-for="content in item.content" :key="content">{{item.name+content}}</li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll';
import Axios from 'axios';
import '../../mockjs';

export default {
  data() {
    return {
      left: null,
      right: null,
      scroll: null,
      listHeight: [],
      scrollY: 0, // 当前y轴的高度
    };
  },
  computed: {
    currentIndex() {
      for (let i = 0, len = this.listHeight.length; i < len; i += 1) {
        const currentHeight = this.listHeight[i];
        const nextHeight = this.listHeight[i + 1];
        if (!nextHeight || (this.scrollY >= currentHeight && this.scrollY < nextHeight)) {
          return i;
        }
      }
      return 0;
    },
  },
  methods: {
    _initScroll() {
      this.lefts = new Bscroll(this.$refs.left, {
        click: true,
      });
      this.rights = new Bscroll(this.$refs.right, {
        probeType: 3,
      });
      this.rights.on('scroll', (pos) => {
        this.scrollY = Math.abs(Math.round(pos.y));
      });
    },
    _getHeight() {
      const rightItems = this.$refs.right.getElementsByClassName('right-item-hook');
      let height = 0;
      this.listHeight.push(height);
      for (let i = 0, len = rightItems.length; i < len; i += 1) {
        height += rightItems[i].clientHeight;
        this.listHeight.push(height);
      }
    },
    selectItem(index, event) {
      // 在better-scroll的派发事件的event和普通浏览器的点击事件event有个属性区别_constructed
      // 浏览器原生点击事件没有_constructed所以当时浏览器监听到该属性的时候return掉
      if (event._constructed) {
        const rightItems = this.$refs.right.getElementsByClassName('right-item-hook');
        const ele = rightItems[index];
        this.rights.scrollToElement(ele, 300);
      } else {
        return false;
      }
      return true;
    },
  },
  mounted() {
    Axios.get('https://api.office.bzdev.net/scroll.json')
      .then((response) => {
        this.left = response.data.dataLeft;
        this.right = response.data.dataRight;
        this.$nextTick(() => {
          this._initScroll();
          this._getHeight();
        });
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style lang="less" scoped>
  @rem: 1/40rem;
  .dome {
    position: relative;
    width: 100%;
    &--title {
      display: block;
      width: 100%;
      border-bottom: 4*@rem solid #999999;
    }
    &__wrapper {
      width: 100%;
      display: flex;
      overflow: hidden;
      position: absolute;
      top: 204*@rem;
      bottom: 100*@rem;
      border-bottom: 4*@rem solid #999999;
      &--left {
        flex: 0 0 160*@rem;
        width: 160*@rem;
        &--item {
          display: block;
          width: 100%;
          height: 200*@rem;
          line-height: 100*@rem;
          text-align: center;
          background-color: #f3f5f7;
          border-bottom: 4*@rem solid #ff55cc;
         }
      }
      .current {
        background-color: #ff55cc;
      }
      &--right {
        flex: 1;
        &--item {
          background-color: #fff;
          li {
            width: 100%;
            height: 200*@rem;
            line-height: 200*@rem;
            text-align: center;
            border-bottom: 2*@rem solid #ff55cc;
          }
        }
      }
    }
  }
</style>
```

``` js
// mockjs/index.js
import Mock from 'mockjs';

const scroll = Mock.mock('https://api.office.bzdev.net/scroll.json', {
  'dataLeft|6': [{
    'name|+1': ['a', 'b', 'c', 'd', 'e', 'f']
  }],
  'dataRight|6': [{
    'name|+1': ['a', 'b', 'c', 'd', 'e', 'f'],
    'content': ['1', '2', '3', '4', '5']
  }],
});

JSON.stringify(scroll, null, 4);
```

### 例子二：上拉加载和下拉刷新

#### 添加配置项

pullup 的配置项`pullUpLoad`

pulldown 的配置项`pullDownRefresh`

#### 基本配置

``` vue
<script>
	export default {
    data() {
      return {};
    },
    methods: {
      initScroll() {
        this.scroll = new BScroll('.dome-wrapper', {
          scrollY: true,
          pullDownRefresh: true,
          pullUpLoad: true,
        });
        this.scroll.on('pullingUp', () => {
          console.log('上拉加载');
          this.scroll.finishPullUp();
        });
      },
    },
  };
</script>
```

【切记】

- 在添加事件时，一定要在回调的最后调用`finishPullUp()` 和`finishPullDown()` 方法来告诉BScroll 一次上拉加载和下拉刷新动作结束，否则上拉加载和下拉刷新效果只会触发一次
- 如果wrapper 里面的结构发生变化一定要调用`refresh()` 方法重新初始化BScroll，否则会导致滑动异常



