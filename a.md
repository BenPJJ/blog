``` js
/**
     * 添加历史事件
     */
addHistory(fn) {
      if (window.history && window.history.pushState) {
        let self = this;
        if (Bzlogin.isWx()) {
          window.addEventListener('pageshow', () => {
            this.timer = setTimeout(() => {
              self.bool = true;
            }, 1000);
          })
        } else {
          self.bool = true;
        }
        let state = {
          title: 'title',
          url: window.location.hash
        };
        window.history.pushState(state, null, window.location.hash);
        window.addEventListener('popstate', fn, false);
      }
    }


 // mounted() {
  //   this.addHistory(this.backChange);
  // },
  // destroyed() {
  //   window.removeEventListener('popstate', this.backChange, false);
  //   clearTimeout(this.timer);
  // }
```

