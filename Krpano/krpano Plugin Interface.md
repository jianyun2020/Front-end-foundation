
# krpano会调用的公共函数

- `registerplugin`：当插件加载的时候krpano会调用此函数，这个函数提供`krpano Interface Object` 和 `krpano Plugin Object`。
- `unloadplugin`：当插件被移除时，krpano会调用此函数。
- `onresize`：`[可选]` 插件元素大小变化时触发。