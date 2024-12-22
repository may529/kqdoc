# kqdoc
前端组件使用文档
1. 用kqui实现如图效果的react页面，所以要引入import React from 'react';
2. 你应优先使用kqui组件来实现，尽可能用kqui的组件及其属性的设置来实现页面效果
3. 当kqui组件不满足需求时，用remax的组件实现。
4. 页面应按kqui的开发规范。避免使用行内样式
5. 图片地址应该本地才用如import img from 'xxx'的形式，图片的src={img} 或src={远程静态资源}
6. 布局尽量使用kqui的Space组件
7. 避免使用html原生标签, 要用到span的地方可以用remax的Text，要用到div的地方可以用用remax的View
