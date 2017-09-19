# TAYGO Challenge

## Changes made

### node_modules/draft-js-inline-toolbar-plugin/lib/components/Toolbar/index.js

original:
```javascript
return _ret = (_temp = (_this = _possibleConstructorReturn(this, (_ref = Toolbar.__proto__ || Object.getPrototypeOf(Toolbar)).call.apply(_ref, [this].concat(args))), _this), _this.state = {
  isVisible: false
}, _this.onVisibilityChanged = function (isVisible) {
  // need to wait a tick for window.getSelection() to be accurate
  // when focusing editor with already present selection
  setTimeout(function () {
    var position = void 0;
    if (isVisible) {
      var relativeParent = getRelativeParent(_this.toolbar.parentElement);
      var relativeRect = relativeParent ? relativeParent.getBoundingClientRect() : document.body.getBoundingClientRect();
      var selectionRect = (0, _draftJs.getVisibleSelectionRect)(window);      

      position = {
        top: selectionRect.top - relativeRect.top - toolbarHeight,
        left: selectionRect.left - relativeRect.left + selectionRect.width / 2,        
        transform: 'translate(-50%) scale(1)',
        transition: 'transform 0.15s cubic-bezier(.3,1.2,.2,1)'
      };
    } else {
      position = { transform: 'translate(-50%) scale(0)' };
    }
    _this.setState({ position: position });
  }, 0);
}, _temp), _possibleConstructorReturn(_this, _ret);
```
changed:
```javascript
return _ret = (_temp = (_this = _possibleConstructorReturn(this, (_ref = Toolbar.__proto__ || Object.getPrototypeOf(Toolbar)).call.apply(_ref, [this].concat(args))), _this), _this.state = {
  isVisible: false
}, _this.onVisibilityChanged = function (isVisible) {
  // need to wait a tick for window.getSelection() to be accurate
  // when focusing editor with already present selection
  setTimeout(function () {
    var position = void 0;
    if (isVisible) {
      var relativeParent = getRelativeParent(_this.toolbar.parentElement);
      var relativeRect = relativeParent ? relativeParent.getBoundingClientRect() : document.body.getBoundingClientRect();
      var selectionRect = (0, _draftJs.getVisibleSelectionRect)(window);
      var leftPX = selectionRect.left - relativeRect.left + selectionRect.width / 2;

      if (leftPX < 73) {
        leftPX = 81;
      } else if (leftPX > relativeRect.width - 73) {
        leftPX = relativeRect.width - 66;
      }

      position = {
        top: selectionRect.top - relativeRect.top - toolbarHeight,
        left: leftPX,
        transform: 'translate(-50%) scale(1)',
        transition: 'transform 0.15s cubic-bezier(.3,1.2,.2,1)'
      };
    } else {
      position = { transform: 'translate(-50%) scale(0)' };
    }
    _this.setState({ position: position });
  }, 0);
}, _temp), _possibleConstructorReturn(_this, _ret);
```

### node_modules/draft-js-inline-toolbar-plugin/lib/plugin.css

original:

```css
.draftJsToolbar__toolbar__dNtBH {
  left: 50%;
  -webkit-transform: translate(-50%) scale(0);
          transform: translate(-50%) scale(0);
  position: absolute;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 2px;
  box-shadow: 0px 1px 3px 0px rgba(220,220,220,1);
  z-index: 2;
  box-sizing: border-box;
}
```

changed:

```css
.draftJsToolbar__toolbar__dNtBH {
  left: 50%;
  -webkit-transform: translate(-50%) scale(0);
          transform: translate(-50%) scale(0);
  position: absolute;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 2px;
  box-shadow: 0px 1px 3px 0px rgba(220,220,220,1);
  z-index: 2;
  box-sizing: border-box;
  width: 146px;
}
```
