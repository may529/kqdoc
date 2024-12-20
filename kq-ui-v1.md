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

# Space 间距组件

Space 组件可以在子元素之间添加间距，支持水平和垂直方向布局。

## 引入

```tsx
import { Space } from '@kqinfo/ui';
```

## 基础用法

### 水平间距

```tsx
<Space size={16}>
  <View>元素1</View>
  <View>元素2</View>
  <View>元素3</View>
</Space>
```

### 垂直间距

```tsx
<Space size={16} vertical>
  <View>元素1</View>
  <View>元素2</View>
  <View>元素3</View>
</Space>
```

### 自定义间距大小

```tsx
// 使用数字(单位:rpx)
<Space size={20}>
  <View>元素1</View>
  <View>元素2</View>
</Space>
// 使用字符串(可指定单位)
<Space size="16px">
  <View>元素1</View>
  <View>元素2</View>
</Space>
```

## Props

| 参数       | 说明                              | 类型                        | 默认值    |
| ---------- | --------------------------------- | --------------------------- | --------- |
| vertical   | 是否垂直布局                      | `boolean`                   | `false`   |
| size       | 间距大小，数字默认单位为 rpx      | `string | number`           | -         |
| flex       | CSS 的 flex 属性                  | `Property.Flex`             | -         |
| justify    | CSS 的 justify-content 属性       | `Property.JustifyContent`   | -         |
| alignItems | CSS 的 align-items 属性           | `Property.AlignItems`       | `stretch` |
| alignSelf  | CSS 的 align-self 属性            | `Property.AlignSelf`        | -         |
| margin     | CSS 的 margin 属性                | `Property.Margin | number`  | -         |
| padding    | CSS 的 padding 属性               | `Property.Padding | number` | -         |
| flexWrap   | CSS 的 flex-wrap 属性             | `Property.FlexWrap`         | -         |
| hidden     | 是否隐藏                          | `boolean`                   | `false`   |
| ignoreNum  | 在一行第几个时不设置间距          | `number`                    | -         |
| animation  | 由 createAnimation 创建的动画对象 | `any`                       | -         |

组件还支持以下原生属性:

- className
- style
- id
- onTap
- onTouchStart
- onTouchMove
- onTouchEnd
- onTouchCancel
- onLongTap

## 注意事项

1. size 属性传入数字时会自动转换为 rpx 单位
2. 在微信小程序中字符串类型的 size 会自动转为大写
3. 组件会自动过滤掉 undefined、null、false、''等无效的子元素
4. 支持 Fragment 语法

# BackgroundImage 背景图组件

一个简单的背景图容器组件,支持图片预览、自定义内容等功能。

## 使用示例

### 基础用法

```
import {BackgroundImg} from '@kqinfo/ui';
export default () => {
return (
<BackgroundImg
img="https://example.com/bg.jpg"
>
  <View>内容</View>
</BackgroundImg>
);
}
```

### 支持图片预览

```
<BackgroundImg
img="https://example.com/bg.jpg"
isPreviewImage
>
点击可预览图片
</BackgroundImg>
```

### 自定义样式

```
<BackgroundImg
img="https://example.com/bg.jpg"
className={styles.customwrap}
imgProps={{
className: {styles.customImg},
mode: 'aspectFit'
}}
innerProps={{
className: {styles.customInner}
}}
>
自定义样式
</BackgroundImg>
```

## Props

| 参数           | 说明                                  | 类型            | 默认值 |
| -------------- | ------------------------------------- | --------------- | ------ |
| img            | 背景图片URL                           | string          | -      |
| imgProps       | 图片的props,继承自Image组件的所有属性 | ImageProps      | -      |
| innerProps     | 内层View的props                       | ViewProps       | -      |
| isPreviewImage | 是否开启图片预览功能                  | boolean         | false  |
| className      | 外层容器的类名                        | string          | -      |
| children       | 子元素                                | React.ReactNode | -      |

组件还支持传入所有View组件的属性。

## 注意事项

1. 背景图片默认采用 `scaleToFill` 模式,可通过 `imgProps.mode` 修改
2. 点击事件会自动阻止冒泡
3. 开启图片预览功能后,点击会调用预览图片API
4. 内部采用相对定位,图片和内容层都是绝对定位

#  Image 组件

基于 remax/wechat 的 Image 组件封装,增强了图片预览、占位图等功能。

##  使用示例

```
import {Image} from '@kqinfo/ui';
export default () => {
return (
<Image
src="https://example.com/image.jpg"
preview={true}
placeholder="https://example.com/placeholder.jpg"
onTap={(e) => {
console.log('image tapped');
}}
onError={(e) => {
console.log('image load failed');
}}
/>
);
}
```

## Props

| 参数        | 说明                         | 类型            | 默认值 |
| ----------- | ---------------------------- | --------------- | ------ |
| src         | 图片地址                     | string          | -      |
| preview     | 是否支持预览                 | boolean         | false  |
| placeholder | 加载失败时显示的占位图片地址 | string          | -      |
| onTap       | 点击事件回调                 | (event) => void | -      |
| onError     | 加载失败回调                 | (event) => void | -      |

其他属性将透传给 remax/wechat 的 Image 组件。

## 特性

- 支持图片预览功能
- 支持加载失败后显示占位图
- 默认使用 aspectFill 模式展示图片
- 支持点击和错误事件处理

## 注意事项

1. preview 和 onTap 可以同时使用,此时会先触发预览,再执行 onTap 回调
2. 图片加载失败时,会先尝试显示 placeholder 图片,再触发 onError 回调



# 条形码组件

一个基于 JsBarcode 的 React 条形码生成组件。

## 安装

```
npm install jsbarcode
```

## 使用示例

```
import {BarCode} from '@kqinfo/ui';
export default () => {
return (
<BarCode
content="123456789"
style={{ width: '300px', height: '100px' }}
webProps={{
fontSize: 20,
width: 1.5
}}
/>
);
}
```

## API

### 参数

| 参数     | 说明             | 类型            | 默认值 |
| -------- | ---------------- | --------------- | ------ |
| content  | 条形码内容       | `string`        | -      |
| style    | 容器样式         | `CSSProperties` | -      |
| webProps | JsBarcode 配置项 | `object`        | -      |

### webProps 配置项

| 参数         | 说明                   | 类型      | 默认值 |
| ------------ | ---------------------- | --------- | ------ |
| displayValue | 是否显示条形码原始值   | `boolean` | `true` |
| textMargin   | 条形码和文本之间的间距 | `number`  | `5`    |
| fontSize     | 文本大小               | `number`  | `30`   |
| width        | 条之间的宽度           | `number`  | `2`    |

更多 JsBarcode 配置项请参考: [JsBarcode Options](https://github.com/lindell/JsBarcode/wiki/Options)

## 注意事项

1. 组件会自动将条形码设置为容器的 100% 宽高
2. 条形码默认带有白色背景
3. content 参数为必填项


# QR Code 组件

一个支持点击展示弹窗的二维码组件。

## 使用示例

```
import { QrCode } from '@kqinfo/ui';
export default () => {
return (
<QrCode
content="https://example.com"
showModal={true}
modalTitle="二维码"
onTap={(e) => {
console.log('QR code clicked');
}}
/>
);
}
```

## API

### Props

| 参数       | 说明                 | 类型                 | 默认值  |
| ---------- | -------------------- | -------------------- | ------- |
| content    | 二维码内容           | `string`             | -       |
| showModal  | 是否支持点击展示弹窗 | `boolean`            | `false` |
| modalTitle | 弹窗标题             | `string`             | -       |
| onTap      | 点击二维码的回调函数 | `(e: Event) => void` | -       |

### Ref

组件支持通过 ref 调用以下方法:

```
interface QrCodeRef {
setVisible: (visible: boolean) => void; // 控制弹窗显示/隐藏
}
```

示例:

```
import { QrCode } from '@kqinfo/ui';
import { useRef } from 'react';
export default () => {
const qrRef = useRef<QrCodeRef>(null);
return (
<>
<QrCode
ref={qrRef}
content="https://example.com"
showModal={true}
/>
<button onClick={() => qrRef.current?.setVisible(true)}>
显示二维码
</button>
</>
);
}
```

## 注意事项

1. 当 `showModal` 为 `true` 时,点击二维码会自动显示弹窗
2. 可以通过 ref 手动控制弹窗的显示/隐藏
3. `onTap` 回调会在点击二维码时触发,无论是否显示弹窗




## 图标组件

### Icon 

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


## 按钮组件

### Button 

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

## 分块标题组件

### PartTitle

#### 一般用法

效果图：

<img width="318" alt="image" src="https://github.com/user-attachments/assets/3443b366-386c-4eca-8bd2-e6461e072e7b" />



```
    <PartTitle>一般用法</PartTitle>
    <PartTitle required>必填</PartTitle>
    <PartTitle required bold={false}>
      必填细体
    </PartTitle>
    <PartTitle required bold={false} full>
      填充字体颜色
    </PartTitle>
    <PartTitle required bold={false} round>
      圆角
    </PartTitle>
    <PartTitle
      required
      bold={false}
      full
      action={<Button type={'action'}>操作</Button>}
    >
      操作按钮
    </PartTitle>
  
```

#### API

| 属性名    | 描述                       | 类型            | 默认值 |
| :-------- | :------------------------- | :-------------- | :----- |
| required  | 显示必填的星号             | `boolean`       | `-`    |
| bold      | 是否加粗文字               | `boolean`       | `true` |
| className | -                          | `string`        | `-`    |
| full      | 是否填充字体颜色           | `boolean`       | `-`    |
| offsetX   | 左边偏移量，rpx单位        | `number`        | `-`    |
| elderly   | 适老模式，开启后尺寸会变大 | `boolean`       | `-`    |
| action    | 标题右侧操作               | `ReactNode`     | `-`    |
| style     | 样式                       | `CSSProperties` | `-`    |
| round     | 圆角样式                   | `boolean`       | `-`    |


## 温馨提示题组件

### Tip

#### 一般用法

效果图：

<img width="314" alt="image" src="https://github.com/user-attachments/assets/9c42fe73-69c6-4df4-a28e-ecedf5da5c56" />



```
   <Tip
      items={[
        <Space style={{ color: '#D95E38', marginBottom: 20 }}>
          请在预约时间段内携带本人身份证前往医院登记台完成登记与接种
        </Space>,
        '1、3-7天之内不宜饮酒',
        '2、不宜剧烈运动，应注意休息',
        '3、一周内避免接触个人既往过敏物及常见致敏源',
        '4、一周内不宜进食辛辣刺激或海鲜类食物，建议清淡饮食',
      ]}
    />
  
```

#### API

| 属性名     | 描述                                                  | 类型                                                         | 默认值       |
| :--------- | :---------------------------------------------------- | :----------------------------------------------------------- | :----------- |
| items      | 提示项                                                | `ReactNode[]`                                                | `(必选)`     |
| title      | 提示标题                                              | `ReactNode`                                                  | `温馨提示：` |
| iconColor  | 图标颜色                                              | `string`                                                     | `#FABD52`    |
| icon       | 图标                                                  | `ReactNode`                                                  | `kq-tip`     |
| elderly    | 适老模式，开启后尺寸会变大                            | `boolean`                                                    | `-`          |
| vertical   | 是否垂直                                              | `boolean`                                                    | `false`      |
| children   | 子元素                                                | `ReactNode | ReactNodeArray`                                 | `-`          |
| size       | 间距大小，字符串可以传入自定义单位，数字默认会转为rpx | `string | number`                                            | `-`          |
| flex       | CSS的flex设置                                         | `Flex<0 | (string & {})>`                                    | `-`          |
| justify    | CSS的justify设置                                      | `JustifyContent`                                             | `-`          |
| alignItems | CSS的alignItems设置                                   | `AlignItems`                                                 | `stretch`    |
| alignSelf  | CSS的alignSelf设置                                    | `AlignSelf`                                                  | `-`          |
| margin     | CSS的margin设置                                       | `number | "-moz-initial" | "inherit" | "initial" | "revert" | "unset" | "auto" | (string & {})` | `-`          |
| padding    | CSS的padding设置                                      | `number | "-moz-initial" | "inherit" | "initial" | "revert" | "unset" | (string & {})` | `-`          |
| flexWrap   | CSS的flexWrap设置                                     | `FlexWrap`                                                   | `-`          |
| hidden     | -                                                     | `boolean`                                                    | `-`          |
| ignoreNum  | 在一行第几个时不设置size                              | `number`                                                     | `-`          |
| animation  | 由createAnimation创建的动画对象                       | `any`                                                        | `-`          |
| style      | -                                                     | `CSSProperties`                                              | `-`          |
| className  | -                                                     | `string`                                                     | `-`          |

#### 自定义类名

| 属性名   | 描述     | 类型     | 默认值 |
| :------- | :------- | :------- | :----- |
| textCls  | 文字类名 | `string` | `-`    |
| iconCls  | 图标类名 | `string` | `-`    |
| titleCls | 标题类名 | `string` | `-`    |


## 时间线组件

### TimeLine

#### 一般用法

效果图：

<img width="314" alt="image" src="https://github.com/user-attachments/assets/f7976167-5ad1-42fb-a71f-b72fcbcf5e5c" />




```
    <TimeLine
      data={[
        {
          state: 'done',
          title: '已签收',
          detail: '您的订单已由本人签收，感谢您在xx购物，欢迎再次光临',
          date: '2019-05-03 12:11:18',
        },
        {
          state: 'pending',
          title: '派送中',
          detail: (
            <Text>
              您的快递正在派送中，快递员xx，电话
              <ColorText>1234568978</ColorText>
            </Text>
          ),
          date: '2019-05-03 11:11:11',
        },
        {
          state: 'pending',
          title: '运输中',
          detail: '您的订单已到达【重庆中渝广场】',
          date: '2019-05-03 09:10:25',
        },
        {
          state: 'pending',
          title: '运输中',
          detail: '您的订单已揽件',
          date: '2019-05-01 11:11:11',
        },
      ]}
    />
  
```

#### API

| 属性名    | 描述           | 类型            | 默认值   |
| :-------- | :------------- | :-------------- | :------- |
| className | -              | `string`        | `-`      |
| data      | 菜单数据       | `Data[]`        | `(必选)` |
| style     | 样式           | `CSSProperties` | `-`      |
| doneIcon  | 自定义完成图标 | `ReactNode`     | `-`      |

#### 自定义类名

| 属性名      | 描述             | 类型     | 默认值 |
| :---------- | :--------------- | :------- | :----- |
| dotCls      | 时间点类名       | `string` | `-`    |
| doneIconCls | 完成图标类名     | `string` | `-`    |
| lineCls     | 线类名           | `string` | `-`    |
| titleCls    | 标题类名         | `string` | `-`    |
| detailCls   | 详情类名         | `string` | `-`    |
| dateCls     | 日期类名         | `string` | `-`    |
| activeCls   | 当前时间详情类名 | `string` | `-`    |
| itemCls     | 子项类名         | `string` | `-`    |

