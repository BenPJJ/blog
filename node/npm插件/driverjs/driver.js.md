# driver.js

使用driver.js来进行页面分步引导

## 安装

``` js
npm install --save driver.js
```

或者直接在文件中引入

``` js
<link rel="stylesheet" href="/dist/driver.min.css">
<script src="/dist/driver.min.js"></script>
```

## 基本配置

``` js
npm install --save driver.js
```

或者直接在文件中引入

``` js
<link rel="stylesheet" href="/dist/driver.min.css">
<script src="/dist/driver.min.js"></script>
```

``` js
import Driver from 'driver.js';
import 'driver.js/dist/driver.min.css';

export default {
  data() {
    return {
      driver: null,
    };
  },
 	mounted() {
    this.driver = new Driver();
  },
};
```

## 突出显示单个元素

传递选择器即可突出显示单个元素

``` js
this.driver.highlight('#CMS');
```

## 突出显示和弹出框

``` js
this.driver.highlight({
  element: '#CMS',
  popover: {
    title: 'Title for the Popover',
    description: 'Description for it',
  },
});
```

## 定位弹出框

``` js
this.driver.highlight({
  element: '#CMS',
  popover: {
    title: 'Title for the Popover',
    description: 'Description for it',
    position: 'left', // 可以使用top、left、right、bottom
  },
});
```

## Example

``` js
// guide.js
const guide = [
  {
    element: '#guide',
    popover: {
      title: 'zsys操作指南',
      description: '操作指引流程',
    },
  },
  // ...
];
export default guide;
```

``` vue
import Driver from 'driver.js';
import 'driver.js/dist/driver.min.css';
import guide from '../assets/js/guide';

export default {
	data() {
		return {
			driver: null,
		};
	},
	methods: {
		guide() {
			this.driver.defineSteps(guide);
      this.driver.start();
		},
	},
	mounted() {
		this.driver = new Driver({
      nextBtnText: '下一步',
      prevBtnText: '上一步',
      closeBtnText: '关闭',
      doneBtnText: '完成',
      allowClose: false,
    });
	},
};
```

