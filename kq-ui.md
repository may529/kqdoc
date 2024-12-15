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

### 布局组件

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
| hidden     | 是否隐藏                                                     | `boolean`                                                    | `-`       |
| ignoreNum  | 在一行第几个时不设置size                              | `number`                                                     | `-`       |
| animation  | 由createAnimation创建的动画对象                       | `any`                                                        | `-`       |
| style      | 行内样式                                                     | `CSSProperties`                                              | `-`       |
| className  | 样式名                                                     | `string`                                                     | `-`       |
| ref        | -                                                     | `Ref<unknown>`                                               | `-`       |
| key        | -                                                     | `Key`                                                        | `-`       |


## Icon 

### 图标组件

#### 一般用法

效果图：

<img width="32" alt="image" src="https://github.com/user-attachments/assets/25b4701e-febb-455c-87c6-d455237a2dbb" />


```
<Icon name={'kq-sousuo'} size={40} color={'#333'} />
```

#### 图标库：如下是图标所对应的name以及对应的效果图


|      |      |
| ---- | ---- |
|   <img width="291" alt="image" src="https://github.com/user-attachments/assets/b2126084-ead6-40c6-b7c2-338741473c62" />   |   <img width="282" alt="image" src="https://github.com/user-attachments/assets/3f51099c-5ba5-46ab-ac63-80c9918a093b" />   |
|   <img width="284" alt="image" src="https://github.com/user-attachments/assets/e3b34089-24e1-466a-a45f-130dea8fc792" />
   |   <img width="285" alt="image" src="https://github.com/user-attachments/assets/5bb5036e-2bc7-4e8a-828b-b22cd2f067c6" />
   |
|      |      |




#### API

| 属性名    | 描述                                                      | 类型                | 默认值   |
| :-------- | :-------------------------------------------------------- | :------------------ | :------- |
| size      | 图标大小，默认是fontSize的值，传入number的话请输入rpx的值 | `string | number`   | `-`      |
| className | 样式名                                                         | `string`            | `-`      |
| style     | 行内样式                                                        | `CSSProperties`     | `-`      |
| name      | 图标name                                                         | `IconFontNames`     | `(必选)` |
| color     | 图标颜色                                                         | `string | string[]` | `-`      |


## Button 

### 按钮组件

#### 按钮类型

默认
<img width="311" alt="image" src="https://github.com/user-attachments/assets/54df326e-7b4a-4b1d-8d80-614928ade7bd" />




```
<Button>默认</Button>
```

主题色按钮

<img width="308" alt="image" src="https://github.com/user-attachments/assets/b46352a6-c83e-45ea-96e2-77893d17f6c6" />



```
<Button type={'primary'}>主题色按钮</Button>
```

醒目色按钮

<img width="305" alt="image" src="https://github.com/user-attachments/assets/01a5d881-a4c6-4970-855e-6bcc4079a6de" />



```
<Button type={'attract'}>醒目色按钮</Button>
```

#### 幽灵按钮

默认

<img width="308" alt="image" src="https://github.com/user-attachments/assets/8f03cb97-3596-4399-9fc7-7bdc8dc302ac" />



```
<Button ghost>默认</Button>
```

主题色按钮

<img width="309" alt="image" src="https://github.com/user-attachments/assets/1bee4876-8347-4e02-93a3-293f76121134" />



```
<Button type={'primary'} ghost>
      主题色按钮
</Button>
```

醒目色按钮

<img width="309" alt="image" src="https://github.com/user-attachments/assets/9c7117a2-4e27-4382-9f57-c78bb218a2c9" />



```
<Button type={'attract'} ghost>
      醒目色按钮
</Button>
```

#### 阴影

默认


<img width="316" alt="image" src="https://github.com/user-attachments/assets/6f08a6e8-e96d-45f6-8d77-0c3f32fa8ea1" />


```
<Button shadow>默认</Button>
```

主题色按钮

<img width="309" alt="image" src="https://github.com/user-attachments/assets/51153c2c-653e-4aeb-b2da-1d8f7e117a55" />



```
<Button type={'primary'} shadow>
      主题色
</Button>
```

醒目色按钮

<img width="309" alt="image" src="https://github.com/user-attachments/assets/11924014-6b2c-4d47-b08e-d9636914c333" />



```
<Button type={'attract'} shadow>
      醒目色
</Button>
```

#### 

#### 行内元素按钮

默认/主题色按钮/醒目色按钮


<img width="270" alt="image" src="https://github.com/user-attachments/assets/b5f181e3-2bc2-48c2-a4dd-213bd9c86ca3" />


```
<Button block={false}>默认</Button>
<Button type={'primary'} block={false}>
        主题色按钮
</Button>
<Button type={'attract'} block={false}>
        醒目色按钮
</Button>
```

#### 按钮大小

小号/操作按钮/最小的按钮


<img width="234" alt="image" src="https://github.com/user-attachments/assets/e77bd8a1-289a-4197-9458-496704a6712b" />


```
<Button size={'small'} block={false}>
        小号
</Button>
<Button type={'primary'} size={'action'} block={false}>
        操作按钮，大小跟小号差不多
</Button>
<Button type={'primary'} size={'tiny'} block={false}>
        最小的按钮
</Button>
```

#### 按钮组

<img width="104" alt="image" src="https://github.com/user-attachments/assets/45166eb7-997d-403a-9104-e71b86ead946" />



```
<Button.Group>
        <Button type={'primary'} size={'small'}>
          提交
        </Button>
        <Button type={'attract'} size={'small'}>
          返回
        </Button>
</Button.Group>
```

圆角按钮组

<img width="102" alt="image" src="https://github.com/user-attachments/assets/15ea5a51-5276-4eea-a90d-e63068b10a2a" />


```
<Button.Group>
        <Button type={'primary'} size={'small'}>
          提交
        </Button>
        <Button type={'attract'} size={'small'}>
          返回
        </Button>
</Button.Group>
```
#### 按钮加载中

<img width="315" alt="image" src="https://github.com/user-attachments/assets/aaaca3ff-f36d-4642-a419-a5935f919d97" />



```
 <Button loading>默认</Button>
 <Button loading type={'primary'}>
      主题色按钮
 </Button>
 <Button loading type={'attract'}>
      醒目色按钮
 </Button>
```



#### API

| 属性名    | 描述                                             | 类型                                     | 默认值    |
| :-------- | :----------------------------------------------- | :--------------------------------------- | :-------- |
| block     | 是否是行内元素                                   | `boolean`                                | `true`    |
| size      | 按钮大小                                         | `"normal" | "small" | "action" | "tiny"` | `normal`  |
| shadow    | 阴影                                             | `boolean`                                | `false`   |
| type      | 类型                                             | `"default" | "primary" | "attract"`      | `default` |
| ghost     | 镂空                                             | `boolean`                                | `false`   |
| icon      | 图标                                             | `ReactNode`                              | `-`       |
| bold      | 粗体                                             | `boolean`                                | `false`   |
| disabled  | 禁用                                             | `boolean`                                | `false`   |
| round     | 是否是圆形按钮                                   | `boolean`                                | `false`   |
| loading   | 是否是加载状态                                   | `boolean`                                | `false`   |
| elderly   | 适老模式，开启后不同type的按钮文字和尺寸都会变大 | `boolean`                                | `-`       |
| style     | 行内样式                                               | `CSSProperties`                          | `-`       |
| className | 样式名                                               | `string`                                 | `-`       |
