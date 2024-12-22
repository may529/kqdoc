# kqdoc
前端组件使用文档
1. 用kqui实现如图效果的react页面，所以要引入import React from 'react';
2. 你应优先使用kqui组件来实现，尽可能用kqui的组件及其属性的设置来实现页面效果
3. 当kqui组件不满足需求时，用remax的组件实现。
4. 页面应按kqui的开发规范。避免使用行内样式
5. 图片地址应该本地才用如import img from 'xxx'的形式，图片的src={img} 或src={远程静态资源}
6. 布局尽量使用kqui的Space组件
7. 避免使用html原生标签, 要用到span的地方可以用remax的Text，要用到div的地方可以用用remax的View
8. 尽量避免使用ColorText来包裹有颜色的文字
9. 当区块内容被一个背景图所包裹时，建议才用BackgroundImg组件
10. 看起来像tag的，可以采用Space包裹文字来实现


# 用cursor开发页面
一、预设文档：先在cursor的设置---Features--Doces 添加kqui文档，等文档变绿了，就说明他学习完了
https://github.com/may529/kqdoc/blob/main/kq-ui-v03.md

二、截图：开发的时候，@doces--找到kqui文档。截图设计图贴到cursor上
三、给提示词：按照如下提示词。
1、用kqui实现如图效果的react页面，所以要引入import React from 'react';
2、你应优先使用kqui组件来实现，尽可能用kqui的组件及其属性的设置来实现页面效果
3、当kqui组件不满足需求时，用remax的组件实现。
4、页面应按kqui的开发规范。避免使用行内样式
5、图片地址应该本地才用如import img from 'xxx'的形式，图片的src={img} 或src={远程静态资源}
6、布局尽量使用kqui的Space组件
7、避免使用html原生标签, 要用到span的地方可以用remax的Text，要用到div的地方可以用用remax的View
8、尽量避免使用ColorText来包裹有颜色的文字
9、当区块内容被一个背景图所包裹时，建议才用BackgroundImg组件
10、看起来像tag的，可以采用Space包裹文字来实现

四、调样式：等页面生成的差不多了，就是点击蓝湖设计图上需要美化的区域，贴对应样式过来。同时页面元素的className 与之对应。
