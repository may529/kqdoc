# Kqinfo UI

基于 Remax 全平台 UI 库



## 使用

```
$ yarn add @kqinfo/ui
```



## 按需加载

安装`babel-plugin-import`插件

```
$ yarn add babel-plugin-import -D
```

修改`babel.config.js`文件

```
// babel.config.js
module.exports = {
  plugins: [
+    [
+      'import',
+      {
+        libraryDirectory: 'es',
+        libraryName: '@kqinfo/ui'
+      },
+      '@kqinfo/ui'
+    ]
  ]
};
```

修改`app.tsx`文件

```
+import { ConfigProvider } from '@kqinfo/ui';

const App = (props) => {
-  return props.children;
+  return <ConfigProvider brandAttract={'#ff9d46'} brandPrimary={'#2780d9'}>{props.children}</ConfigProvider>;
};
```

## 开发注意项

- 样式不要嵌套
- 样式用`less-modules`
- 表单组件暴露`value`和 onChange



#### kqinfo ui 的使用将分为两部分来介绍：组件 和 工具

### 组件

## Space

用于各种布局分割的组件，如果没有效果请确保`children`支持`style`的 prop，

默认情况Space 具有flex 横向布局

**横排布局**

效果图：

<img width="305" alt="image" src="https://github.com/user-attachments/assets/b539facb-5c27-456c-854b-fe363db12935" />


```
<Space size={'10px'}> //size是Space内各子元素的间隔
      <Button block={false}>1</Button>
      <Button>2</Button>
      <Button type={'primary'}>3</Button>
</Space>
```

**竖排布局**

效果图：

<img width="307" alt="image" src="https://github.com/user-attachments/assets/d8a4e755-1785-4845-800d-7d05069174b6" />



```
<Space vertical size={'10px'} alignItems={'flex-start'}> //vertical代表竖排布局，alignItems相当于 align-items
      <Button block={false}>1</Button>
      <Button>2</Button>
      <Button type={'primary'}>3</Button>
</Space>
```

我们来构建一个列表子项的布局试试

**列表子项布局**

分析布局：子项分左中右布局。各子项垂直居中对齐，水平间隔10px，左边项宽高固定。中间项宽度弹性布局。右边项固定大小

效果图：

<img width="301" alt="image" src="https://github.com/user-attachments/assets/acc58ef9-c57c-44ff-807f-65c48ed24e2d" />


```
<Space
      size={'10px'}
      style={{ background: '#fff', color: '#333' }}
      alignItems={'center'}
    >
      <div style={{ background: '#eee', width: 50, height: 50 }} />
      <Space flex={1} size={'10px'} vertical>
        <Space>名称</Space>
        <Space>描述</Space>
      </Space>
      <Space style={{ marginRight: 10 }}>操作</Space>
</Space>
```

