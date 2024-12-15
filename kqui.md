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
- 代码中尽可能用CSS Modules，比如使用了 styles.xxx 这种方式来定义className
- 尽量不要写内联样式
- 表单组件暴露`value`和 onChange
- 尽量不要用Image 当 Icon，能用Icon的尽量用Icon



#### kqinfo ui 的使用将分为两部分来介绍：组件 和 工具

### 组件

## Space

用于各种布局分割的组件，如果没有效果请确保`children`支持`style`的 prop，

默认情况Space 具有flex 横向布局

##### 横排布局

效果图：

<img width="305" alt="image" src="https://github.com/user-attachments/assets/b539facb-5c27-456c-854b-fe363db12935" />


```
<Space size={'10px'}> //size是Space内各子元素的间隔
      <Button block={false}>1</Button>
      <Button>2</Button>
      <Button type={'primary'}>3</Button>
</Space>
```

##### 竖排布局

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

##### 列表子项布局

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
##### 网格布局

分析布局：这类布局每个子项大小相同，比如4列网格布局，往往每个子项都占25%，占满一行后需要能自动换行 这里用flexWrap={'wrap'}。由于每个元素有间隔，往往需要在一行的最后一个元素不设置间隔。这里用ignoreNum={4}

效果图：

<img width="291" alt="image" src="https://github.com/user-attachments/assets/bbd3ec31-b617-44f9-ab64-c9faaafc60bd" />


```
  <Space ignoreNum={4} flexWrap={'wrap'} size={'14px'}>
      {new Array(6).fill(0).map((_, i) => (
        <Space
          vertical
          style={{ width: '25%' }}
          size={'10px'}
          alignItems={'center'}
        >
          <Space
            style={{ width: '100%', height: '50px', background: '#eee' }}
          />
          <Space
            style={{
              width: '100%',
              height: '10px',
              background: '#eee',
              marginBottom: '20px',
            }}
          />
        </Space>
      ))}
   </Space>
```

#### API



| 属性名     | 描述                                                  | 类型                                                         | 默认值    |
| :--------- | :---------------------------------------------------- | :----------------------------------------------------------- | :-------- |
| vertical   | 是否垂直                                              | `boolean`                                                    | `false`   |
| children   | 子元素                                                | `ReactNode | ReactNodeArray`                                 | `-`       |
| size       | 间距大小，字符串可以传入自定义单位，数字默认会转为rpx | `string | number`                                            | `-`       |
| flex       | CSS的flex设置                                         | `Flex<0 | (string & {})>`                                    | `-`       |
| justify    | CSS的justify设置                                      | `JustifyContent`                                             | `-`       |
| alignItems | CSS的alignItems设置                                   | `AlignItems`                                                 | `stretch` |
| alignSelf  | CSS的alignSelf设置                                    | `AlignSelf`                                                  | `-`       |
| margin     | CSS的margin设置                                       | `number | "-moz-initial" | "inherit" | "initial" | "revert" | "unset" | "auto" | (string & {})` | `-`       |
| padding    | CSS的padding设置                                      | `number | "-moz-initial" | "inherit" | "initial" | "revert" | "unset" | (string & {})` | `-`       |
| flexWrap   | CSS的flexWrap设置                                     | `FlexWrap`                                                   | `-`       |
| hidden     | -                                                     | `boolean`                                                    | `-`       |
| ignoreNum  | 在一行第几个时不设置size                              | `number`                                                     | `-`       |
| animation  | 由createAnimation创建的动画对象                       | `any`                                                        | `-`       |
| style      | -                                                     | `CSSProperties`                                              | `-`       |
| className  | -                                                     | `string`                                                     | `-`       |
| ref        | -                                                     | `Ref<unknown>`                                               | `-`       |
| key        | -                                                     | `Key`                                                        | `-`       |

## Icon

### 图标

#### 一般用法

效果图：

<img width="32" alt="image" src="https://github.com/user-attachments/assets/25b4701e-febb-455c-87c6-d455237a2dbb" />


```
<Icon name={'kq-sousuo'} size={40} color={'#333'} />
```

图标库：如下是图标所对应的name以及对应的效果图
| name      | 图标效果图                                                |
| :-------- | :-------------------------------------------------------- |
| kq-search | <img width="35" alt="image" src="https://github.com/user-attachments/assets/2284da7c-2e7e-4b9f-8777-b8560c3b1e3c" /> |
| kq-loading | <img width="29" alt="image" src="https://github.com/user-attachments/assets/b96d3563-4e76-47ce-b841-bd33c543d335" />
 |
| kq-down | <img width="21" alt="image" src="https://github.com/user-attachments/assets/8ec19bb8-ca6e-47f8-8fc9-29ed7d1e52a0" /> |
| kq-loading2 | <img width="34" alt="image" src="https://github.com/user-attachments/assets/0054f7c8-7a7f-434a-b1cf-dae53f758d17" />
 |
| kq-yes | <img width="26" alt="image" src="https://github.com/user-attachments/assets/a3153396-6170-4491-83f7-cb0bce423159" />
 |
| kq-add | <img width="24" alt="image" src="https://github.com/user-attachments/assets/ea798de5-0054-4316-b0ca-6e2f8851d874" />
|
| kq-clear | <img width="31" alt="image" src="https://github.com/user-attachments/assets/6cff80b9-a16c-4316-897e-a593d456f521" />
 |
| kq-clear2 | <img width="26" alt="image" src="https://github.com/user-attachments/assets/0126ef85-c8a4-4631-9dfb-5aa826c3645d" />
 |
| kq-notice | <img width="24" alt="image" src="https://github.com/user-attachments/assets/8d3a9b77-dd58-4fde-949f-a4b5eac54a9c" />
 |
| kq-zengjia | <img width="26" alt="image" src="https://github.com/user-attachments/assets/357895d8-826b-4c8e-aa53-8197c2a53d1f" />
 |



## API

| 属性名    | 描述                                                      | 类型                | 默认值   |
| :-------- | :-------------------------------------------------------- | :------------------ | :------- |
| size      | 图标大小，默认是fontSize的值，传入number的话请输入rpx的值 | `string | number`   | `-`      |
| className | -                                                         | `string`            | `-`      |
| style     | -                                                         | `CSSProperties`     | `-`      |
| name      | -                                                         | `IconFontNames`     | `(必选)` |
| color     | -                                                         | `string | string[]` | `-`      |

