# 判断wap端和pc端

``` vue
export default {
	data() {
		const ua = window.navigator.userAgent;
		return {
			isPc: !/(iPhone|iPod|iPad|iOS|Android|SymbianOS)/i.test(ua),
			isIos: /(iPhone|iPod|iPad|iOS)/i.test(ua),
		},
	},
};
```

