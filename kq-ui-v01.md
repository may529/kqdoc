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

<img width="314" alt="image" src="https://github.com/user-attachments/assets/5127e3aa-f92f-429c-bd56-489cc5a5cdac" />


```tsx
<Space size={16}>
  <View>元素1</View>
  <View>元素2</View>
  <View>元素3</View>
</Space>
```

### 垂直间距

<img width="316" alt="image" src="https://github.com/user-attachments/assets/55e1d758-b72c-4dfe-a512-c02b765dfbe2" />


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

<img width="265" alt="image" src="https://github.com/user-attachments/assets/f4e31935-b245-41c0-ad05-2ac20518a0cc" />


```
import {BackgroundImg} from '@kqinfo/ui';
export default () => {
return (
<BackgroundImg
img="https://example.com/bg.jpg"
>
  <View>
   <View>基础护理</View>
   <View>肌肉注射雾化</View>
  </View>
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
<img width="100" alt="image" src="https://github.com/user-attachments/assets/5ccbfdcf-d639-4d03-8fd0-8c22ba592dde" />


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

<img width="171" alt="image" src="https://github.com/user-attachments/assets/871ad7db-4eae-4f99-8642-6da67ec994fe" />


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
<img width="310" alt="image" src="https://github.com/user-attachments/assets/997a41af-395c-40e8-aea7-708412f55e10" />


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




# Icon 图标组件

一个跨平台的图标组件,支持自定义大小、颜色,并对loading图标提供了自动旋转效果。

## 使用示例
```
import {Icon} from '@kqinfo/ui';

// 基础用法
<Icon name="home" />
// 自定义颜色和大小
<Icon
name="user"
color="#1890ff"
size={32} // 这里传入的是rpx值
/>
// 使用其他CSS单位
<Icon
name="settings"
size="2em"
/>
// Loading图标(自动旋转)
<Icon name="kq-loading" />

```

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


## 特殊说明

1. size属性说明:
   - 传入number类型时按rpx单位处理
   - 传入string类型时直接作为CSS尺寸值使用
   - 默认值为'1em'

2. 自动旋转:
   - 当图标name为'kq-loading'或'kq-loading2'时会自动添加旋转动画

3. 平台兼容:
   - 在微信小程序中会自动处理rpx/px单位转换
   - 其他平台保持原有单位

4. 样式覆盖:
   - 可以通过className和style属性进行自定义样式设置
   - 组件最外层会添加wrap类名
   - 图标本身会添加icon类名

## 注意事项

1. 在设置size时,建议:
   - 需要固定大小时使用number类型(rpx单位)
   - 需要响应式大小时使用em/rem等相对单位

2. 组件内部会根据平台自动处理单位转换,使用时只需关注业务逻辑

   



# Button 按钮组件

通用按钮组件,支持多种样式类型和状态。

## 引入

```
import { Button } from '@kqinfo/ui';
```

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



## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| type | 按钮类型,可选值为 `default` `primary` `attract` | string | `default` |
| size | 按钮尺寸,可选值为 `tiny` `small` `normal` `action` | string | `normal` |
| block | 是否为块级元素 | boolean | `true` |
| ghost | 是否为镂空按钮 | boolean | `false` |
| disabled | 是否禁用 | boolean | `false` |
| loading | 是否显示加载状态 | boolean | `false` |
| round | 是否为圆形按钮 | boolean | `false` |
| shadow | 是否显示阴影 | boolean | `false` |
| bold | 是否使用粗体 | boolean | `false` |
| elderly | 是否开启适老模式 | boolean | `false` |
| icon | 图标 | ReactNode | - |
| className | 自定义类名 | string | - |
| style | 自定义样式 | CSSProperties | - |
| onTap | 点击事件 | function | - |

### Button.Group Props

Button.Group 继承了 Space 组件的所有属性。

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| className | 自定义类名 | string | - |

## 注意事项

1. 按钮文字过长时会自动换行
2. 开启适老模式后,按钮文字和尺寸会变大
3. 使用 loading 状态时会自动禁用按钮点击


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


# Step 步骤条组件

Step 是一个用于展示步骤/流程的组件，支持自定义样式和交互。

<img width="299" alt="image" src="https://github.com/user-attachments/assets/0ff9b8b5-f16b-472d-aa7f-9bc76af19cfa" />


## 基础用法

```
  import { Step } from '@kqinfo/ui';
export default () => (
<Step
current={2}
items={['第一步', '第二步', '第三步']}
/>
);
  
```

## 虚线样式

```
import { Step } from '@kqinfo/ui';
export default () => (
<Step
type="dashed"
current={2}
items={['第一步', '第二步', '第三步']}
/>
);
```

## 自定义渲染

```
import { Step } from '@kqinfo/ui';
export default () => (
<Step
current={2}
items={[
(active) => ({
icon: <Icon name="custom-icon" />,
text: active ? '已完成' : '第一步'
}),
'第二步',
'第三步'
]}
/>
);

```


## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| current | 当前步骤索引，从1开始 | `number` | - |
| type | 预置样式类型 | `'normal' \| 'dashed'` | `'normal'` |
| items | 步骤配置项 | `(ReactNode \| ((active: boolean) => {icon: ReactNode, text: ReactNode}))[]` | - |
| activeColor | 激活状态的颜色 | `string` | `'#fff'` |
| backgroundColor | 背景颜色 | `string` | `brandPrimary` |
| defaultColor | 默认文字/图标颜色 | `string` | - |
| onChoose | 步骤点击事件 | `(index: number) => void` | - |
| className | 容器类名 | `string` | - |
| style | 容器样式 | `CSSProperties` | - |
| itemCls | 步骤项类名 | `string` | - |
| activeItemCls | 激活状态的步骤项类名 | `string` | - |
| dotCls | 圆点类名 | `string` | - |
| lineCls | 连接线类名 | `string` | - |
| activeLineCls | 激活状态的连接线类名 | `string` | - |

### items 类型说明

items 数组的每一项可以是:

1. ReactNode - 直接渲染的内容
2. (active: boolean) => {icon, text} - 函数返回对象:
   - icon: 自定义图标
   - text: 步骤文本

## 注意事项

1. current 从1开始计数
2. type="dashed" 时会显示虚线连接
3. 可以通过 activeColor 和 backgroundColor 配置主题色
4. items 支持函数式配置，可以根据激活状态动态渲染


# Divider 分割线

一个用于分隔内容的组件,支持在内容两侧显示分割线。

<img width="156" alt="image" src="https://github.com/user-attachments/assets/5688f811-1425-4241-b7ca-65d3768485f2" />

## 代码示例

### 基础用法

```
import { Divider } from '@kqinfo/ui';
export default () => (
<Divider>分割文本</Divider>
);
```


### 自定义颜色

```
import { Divider } from '@kqinfo/ui';
export default () => (
<Divider color="#f00">红色分割线</Divider>
);
```

### 隐藏分割线

```
import { Divider } from '@kqinfo/ui';
export default () => (
<Divider hideLine>仅显示文本</Divider>
);
```


## API

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| children | 分割线中的内容 | ReactNode | - |
| color | 分割线和文本的颜色 | string | brandPrimary |
| style | 自定义样式 | CSSProperties | - |
| lineCls | 分割线的自定义类名 | string | - |
| hideLine | 是否隐藏分割线 | boolean | false |

此外还支持 Space 组件的全部属性。

## 注意事项

1. 组件默认使用品牌主色(brandPrimary)作为分割线和文本颜色
2. 文本字号默认为 30rpx
3. 分割线宽度为 1px
4. 组件基于 Space 组件实现,默认居中对齐

# ListItem 列表项组件

一个灵活的列表项组件，支持左侧图片、多行文本内容以及右侧额外内容的展示。

<img width="317" alt="image" src="https://github.com/user-attachments/assets/6963accb-de79-41ca-998a-0d408e0e0453" />


## 组件结构

+----------------+------------------------+-------------+
| | title subtitle | |
| image | text | after |
| imgFooter | footer | |
+----------------+------------------------+-------------+


## 属性说明

### 基础属性
| 属性 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| className | 容器类名 | string | - |

### 左侧区域
| 属性 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| img | 图片地址 | string | - |
| imgCls | 图片类名 | string | - |
| imgFooter | 图片下方内容 | ReactNode | - |
| imgFooterCls | 图片下方内容类名 | string | - |
| leftSpaceProps | 左侧区域Space组件属性 | SpaceProps | - |

### 中间区域
| 属性 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| title | 标题内容 | ReactNode | - |
| titleCls | 标题类名 | string | - |
| subtitle | 副标题内容 | ReactNode | - |
| subtitleCls | 副标题类名 | string | - |
| text | 正文内容 | ReactNode | - |
| textCls | 正文类名 | string | - |
| footer | 底部内容 | ReactNode | - |
| footerCls | 底部内容类名 | string | - |
| rightSpaceProps | 中间区域Space组件属性 | SpaceProps | - |

### 右侧区域
| 属性 | 说明 | 类型 | 默认值 |
|------|------|------|--------|
| after | 右侧内容 | ReactNode | - |
| afterCls | 右侧内容类名 | string | - |

## 使用示例
```
import {ListItem} from '@kqinfo/ui';
export default () => {
return (
<ListItem
img="https://example.com/image.jpg"
imgFooter="图片说明"
title="标题文本"
subtitle="副标题"
text="正文内容"
footer="底部文字"
after="右侧内容"
/>
);
};
```


## 样式定制

组件提供了丰富的类名支持，可以通过以下类名进行样式定制：

- `.item` - 整个列表项容器
- `.img` - 图片
- `.imgFooter` - 图片下方内容
- `.title` - 标题区域
- `.subtitle` - 副标题
- `.text` - 正文
- `.footer` - 底部内容

## 注意事项

1. 组件基于 Space 组件构建，继承了 Space 组件的所有属性
2. 图片默认使用 `aspectFill` 模式展示
3. 所有内容区域都支持传入 ReactNode，可以灵活定制


# List 列表组件

一个功能强大的列表组件,支持加载更多、虚拟滚动、状态管理等特性。

## 特性

- 支持下拉加载更多
- 支持虚拟滚动优化性能
- 内置加载中、空数据、加载失败等状态处理
- 支持数据缓存
- 灵活的自定义渲染

## 代码示例

### 基础用法

```
import { List } from '@kqinfo/ui';
export default () => {
// 获取列表数据
const getList = async ({ page, limit }) => {
const res = await fetch(/api/list?page=${page}&limit=${limit});
return res.json();
};
return (
<List
getList={getList}
renderItem={(item, index) => (
<div key={item.id}>
{index}: {item.name}
</div>
)}
/>
);
};
```

### 虚拟滚动

当列表项较多时,可以开启虚拟滚动优化性能:
```
<List
getList={getList}
renderItem={renderItem}
renderItemHeight={(item) => 100} // 设置每项高度(rpx)
/>
```

### 自定义样式

```
<List
getList={getList}
renderItem={renderItem}
space={{ gap: 10 }} // Space 组件配置
noData={<Empty />} // 自定义空状态
noMore="没有更多了" // 自定义没有更多提示
loadingTip={<Loading />} // 自定义加载提示
/>
```


## Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| getList | 获取列表数据的函数 | `(params: { page: number, limit: number }) => Promise<D[]>` | - |
| renderItem | 渲染列表项 | `(data: D, index: number, list: D[], refreshList: () => void) => ReactElement` | - |
| renderItemHeight | 虚拟滚动时每项高度 | `(data: D, index: number) => number` | - |
| cacheKey | 数据缓存的key | `string` | 当前页面路径 |
| noData | 空数据时的提示 | `ReactNode` | `<NoData/>` |
| noMore | 没有更多时的提示 | `ReactNode` | - |
| loadingTip | 加载提示 | `ReactNode` | `<Loading type="inline"/>` |
| defaultLimit | 每页数量 | `number` | 10 |
| space | Space组件配置 | `SpaceProps` | - |
| style | 自定义样式 | `CSSProperties` | - |
| className | 自定义类名 | `string` | - |

## 方法

通过 ref 可以调用组件方法:
```
const listRef = useRef();
// 刷新列表
listRef.current.refreshList();
<List ref={listRef} {...props} />
```

| 方法名 | 说明 | 参数 |
| --- | --- | --- |
| refreshList | 刷新列表数据 | `(retainList?: boolean) => Promise<void>` |

## 注意事项

1. 虚拟滚动模式下需要正确设置 renderItemHeight
2. getList 返回的数据项需要包含唯一的 id 字段
3. 建议合理使用 cacheKey 来缓存数据,提升用户体验

# NoData 空状态

用于显示暂无数据、加载失败等空状态。

## 何时使用

- 当列表、表格等内容为空时
- 需要占位提示时
- 加载失败需要提示时

## 代码演示
<img width="103" alt="image" src="https://github.com/user-attachments/assets/6d2f852f-1487-48c5-9c39-47993c80e2bb" />

### 基础用法

```
import { NoData } from '@kqinfo/ui';
export default () => {
return <NoData />;
};
```

### 自定义图片

```
import { NoData } from '@kqinfo/ui';
export default () => {
return <NoData src="your-custom-image.png" />;
};
```

### 自定义渲染

通过 ConfigProvider 可以完全自定义空状态的渲染内容：

```
import { ConfigProvider, NoData } from '@kqinfo/ui';
export default () => {
return (
<ConfigProvider
renderNoData={() => <div>自定义的空状态内容</div>}
>
<NoData />
</ConfigProvider>
);
};
```

## API

### Props

| 参数      | 说明           | 类型   | 默认值                                                      |
| --------- | -------------- | ------ | ----------------------------------------------------------- |
| src       | 图片地址       | string | https://kq-static.oss-cn-beijing.aliyuncs.com/ui/noData.png |
| className | 自定义样式类名 | string | -                                                           |

此外，组件还支持所有 Image 组件的属性。

### ConfigProvider

可以通过 ConfigProvider 的 `renderNoData` 属性进行全局配置：

| 参数         | 说明                   | 类型                  | 默认值 |
| ------------ | ---------------------- | --------------------- | ------ |
| renderNoData | 自定义渲染空状态的方法 | () => React.ReactNode | -      |

## 注意事项

1. 当使用自定义渲染时，如果 renderNoData 返回 undefined，将显示默认的空状态图片
2. 组件默认居中显示
3. 可以通过 className 和 style 属性自定义样式

# NoticeBar 通知栏

通知栏组件,用于展示重要的通知信息。支持自定义样式、图标和滚动动画效果。

## 何时使用

- 当需要展示系统通知、消息提醒时
- 需要引起用户注意的重要信息展示
- 营销信息或活动信息的温和提示

## 代码示例
<img width="312" alt="image" src="https://github.com/user-attachments/assets/6d017a1f-f0ce-42ef-9129-07e668cb5d19" />

```
import { NoticeBar } from '@kqinfo/ui';
export default () => {
return (
<NoticeBar
title="通知"
background="#fefcec"
color="#FF9D46"
>
这里是通知内容
</NoticeBar>
);
};
```

## API

| 参数       | 说明                    | 类型                  | 默认值                      |
| ---------- | ----------------------- | --------------------- | --------------------------- |
| className  | 自定义样式名            | `string`              | -                           |
| style      | 行内样式                | `React.CSSProperties` | -                           |
| background | 背景色                  | `string`              | `#fefcec`                   |
| color      | 文字颜色                | `string`              | `#FF9D46`                   |
| icon       | 设置图标,传null则不显示 | `React.ReactNode`     | `<Icon name="kq-notice" />` |
| title      | 设置左侧标题            | `React.ReactNode`     | -                           |
| children   | 消息内容                | `React.ReactNode`     | -                           |

## 注意事项

1. 通知内容过长时会自动开启滚动动画
2. 可以通过传入 `null` 作为 icon 属性来隐藏默认图标
3. title 和 children 支持传入自定义 React 节点
4. 组件样式可以通过 className 和 style 属性进行自定义

# Del 删除线组件

一个用于给文本添加删除线效果的React组件。

## 代码示例
<img width="85" alt="image" src="https://github.com/user-attachments/assets/b5b742b4-15e9-4bf9-bf3b-2fadaccb2f97" />

### 基础用法

```
mport { Del } from '@kqinfo/ui';
export default () => (
<Del>已删除的文本</Del>
);
```

### 自定义样式

```
import { Del } from '@kqinfo/ui';
export default () => (
<Del color="red" style={{fontSize: '20px'}}>
自定义样式的删除文本
</Del>
);
```

## Props

| 参数      | 说明       | 类型                | 默认值  |
| --------- | ---------- | ------------------- | ------- |
| className | 自定义类名 | string              | -       |
| children  | 删除内容   | React.ReactNode     | -       |
| lineCls   | 删除线类名 | string              | -       |
| color     | 删除线颜色 | string              | #999999 |
| style     | 自定义样式 | React.CSSProperties | -       |

## 使用场景

- 显示商品原价
- 标记已删除或失效的内容
- 文本编辑中的删除效果

## 注意事项

1. 组件基于 @kqinfo/ui 的 Space 组件实现
2. 可以通过 color 属性自定义删除线颜色
3. 支持通过 style 和 className 进行样式自定义

# Price 价格组件

一个用于展示价格的 React 组件,支持自定义整数、小数部分的样式,以及价格符号的展示。

## 引入

```
import { Price } from '@kqinfo/ui';
```

## 代码演示
<img width="183" alt="image" src="https://github.com/user-attachments/assets/a36f435a-956e-46da-b425-cb89339e14d9" />

### 基础用法

```
import React from 'react';
import { Price } from '@kqinfo/ui';
export default () => (
<>
<Price price={1234} /> {/ 展示: ¥12.34 /}
<Price price={1234} len={1} /> {/ 展示: ¥12.3 /}
</>
);
```

### 自定义样式

```
import React from 'react';
import { Price } from '@kqinfo/ui';
export default () => (
<Price
price={1234}
bigPrefix // 放大价格符号
bigDecimal // 放大小数部分
bigScale={2} // 设置放大比例
/>
);

```

## API

| 参数       | 说明             | 类型      | 默认值 |
| ---------- | ---------------- | --------- | ------ |
| price      | 金额,单位:分     | `number`  | -      |
| len        | 小数位长度       | `number`  | 2      |
| bold       | 是否使用粗体     | `boolean` | false  |
| bigPrefix  | 是否放大价格符号 | `boolean` | false  |
| bigDecimal | 是否放大小数部分 | `boolean` | false  |
| bigScale   | 字体放大比例     | `number`  | 1.53   |
| bigCls     | 大字体类名       | `string`  | -      |
| integerCls | 整数部分类名     | `string`  | -      |
| decimalCls | 小数部分类名     | `string`  | -      |

## 特性

- 自动处理金额单位转换(分→元)
- 支持自定义小数位数
- 可分别控制价格符号、整数、小数部分的样式
- 灵活的字体大小控制
- 支持自定义 CSS 类名

## 注意事项

1. price 参数接收的金额单位为分
2. 当传入的 price 为 0 或无效值时,将显示 "¥0"
3. bigScale 参数控制放大部分的字体大小比例,如设置为 2 则字体将放大为原来的 2 倍

## 常见问题

Q: 如何只显示整数部分?  
A: 设置 `len={0}` 即可隐藏小数部分

Q: 如何自定义价格符号的样式?  
A: 可以通过 `bigPrefix` 和 `bigCls` 组合使用来自定义价格符号样式

# DownTime 倒计时组件

一个简单的倒计时组件,用于显示距离目标时间的剩余时间。

## 使用示例
<img width="122" alt="image" src="https://github.com/user-attachments/assets/157a0a7d-289a-4a32-85f0-71a47165f55d" />

```
import DownTime from '@kqinfo/ui';
// 基础用法
export default () => {
return (
<DownTime
targetDate="2024-12-31 23:59:59"
format={({d, h, m, s}) => ${d}天${h}时${m}分${s}秒}
/>
);
}
// 自动停止
export default () => {
return (
<DownTime
targetDate="2024-12-31 23:59:59"
format={({d, h, m, s, isEnd}) => {
if(isEnd) return '活动已结束';
return ${d}天${h}时${m}分${s}秒;
}}
autoStop
/>
);
}
```

## API

### Props

| 参数       | 说明                       | 类型                         | 默认值 |
| ---------- | -------------------------- | ---------------------------- | ------ |
| targetDate | 目标日期                   | string                       | -      |
| format     | 自定义格式化函数           | (data: FormatData) => string | -      |
| style      | 自定义样式                 | React.CSSProperties          | -      |
| className  | 自定义类名                 | string                       | -      |
| autoStop   | 是否在倒计时结束后自动停止 | boolean                      | false  |

### FormatData

format 函数的参数类型:

```
interface FormatData {
d: string; // 天数
h: string; // 小时
m: string; // 分钟
s: string; // 秒
diff: number; // 与目标时间差(秒)
isEnd: boolean; // 是否结束
}
```

## 注意事项

1. targetDate 需要是合法的日期字符串格式
2. format 函数必须返回字符串类型
3. 组件会在unmount时自动清理定时器
4. 当autoStop为true时,倒计时结束后会自动停止更新

# ColorText 彩色文本

一个支持自定义颜色、下划线、字体大小和字重的文本组件。

## 介绍

ColorText 是基于 remax/one 的 Text 组件封装,用于显示带有自定义样式的文本内容。默认使用 ConfigProvider 中的 brandPrimary 作为文本颜色。

## 使用示例
<img width="64" alt="image" src="https://github.com/user-attachments/assets/dc1dd1fc-e33f-4da5-920d-dd81c369f73b" />

```
import { ColorText } from '@kqinfo/ui';
export default () => {
return (
<>
{/ 基础用法 /}
<ColorText>默认文本</ColorText>
{/ 自定义颜色 /}
<ColorText color="#ff0000">红色文本</ColorText>
{/ 带下划线 /}
<ColorText underline>带下划线的文本</ColorText>
{/ 自定义字体大小和字重 /}
<ColorText fontSize="20px" fontWeight="bold">
大号加粗文本
</ColorText>
</>
);
};
```

## API

### Props

| 参数       | 说明           | 类型                                | 默认值                           |
| ---------- | -------------- | ----------------------------------- | -------------------------------- |
| color      | 文本颜色       | `string`                            | ConfigProvider 中的 brandPrimary |
| underline  | 是否显示下划线 | `boolean`                           | `false`                          |
| fontSize   | 字体大小       | `string`                            | -                                |
| fontWeight | 字重           | `React.CSSProperties['fontWeight']` | -                                |

此外,组件还支持 remax/one 的 Text 组件的所有原生属性。

## 注意事项

1. 组件默认继承 ConfigProvider 中的 brandPrimary 作为文本颜色
2. 当设置 underline 为 true 时,下划线颜色与文本颜色保持一致
3. fontSize 和 fontWeight 可以通过传入合法的 CSS 值来自定义文本样式

# Search 搜索组件

一个功能完整的搜索输入框组件,支持搜索按钮、清除输入、适老模式等特性。

## 代码示例

### 基础用法
<img width="309" alt="image" src="https://github.com/user-attachments/assets/84d84ab7-2bd5-4e7f-84f5-7a0fb3af7092" />


```
import { Search } from '@kqinfo/ui';
export default () => (
<Search
placeholder="请输入搜索内容"
onConfirm={value => console.log(value)}
/>
);
```

### 显示搜索按钮
<img width="306" alt="image" src="https://github.com/user-attachments/assets/4f616c4b-f7e8-4f36-a6f2-f968a0af0eaa" />


```
import { Search } from '@kqinfo/ui';
export default () => (
<Search
showBtn
placeholder="请输入搜索内容"
onConfirm={value => console.log(value)}
/>
);

```

### 适老模式

```
import { Search } from '@kqinfo/ui';
export default () => (
<Search
elderly
placeholder="请输入搜索内容"
onConfirm={value => console.log(value)}
/>
);
```

## API

### Props

| 参数           | 说明                                | 类型                      | 默认值  |
| -------------- | ----------------------------------- | ------------------------- | ------- |
| showBtn        | 是否显示搜索按钮                    | `boolean`                 | `false` |
| value          | 输入框的值                          | `string`                  | -       |
| onChange       | 输入框内容变化时的回调              | `(value: string) => void` | -       |
| onConfirm      | 点击搜索按钮或按下回车时的回调      | `(value: string) => void` | -       |
| elderly        | 适老模式,开启后按钮文字和尺寸会变大 | `boolean`                 | `false` |
| shadow         | 是否显示阴影效果                    | `boolean`                 | `false` |
| iconColor      | 搜索图标的颜色                      | `string`                  | `#ccc`  |
| className      | 组件容器类名                        | `string`                  | -       |
| style          | 组件容器样式                        | `CSSProperties`           | -       |
| inputWrapCls   | 输入框外层容器类名                  | `string`                  | -       |
| inputWrapStyle | 输入框外层容器样式                  | `CSSProperties`           | -       |
| inputCls       | 输入框类名                          | `string`                  | -       |
| btnCls         | 搜索按钮类名                        | `string`                  | -       |
| btnStyle       | 搜索按钮样式                        | `CSSProperties`           | -       |

## 注意事项

1. 组件默认继承了 Input 组件的所有 Props
2. 适老模式会自动跟随 ConfigProvider 的配置
3. 在 Web 端和原生端清除按钮的显示逻辑略有不同
4. 支持自定义搜索按钮文案和样式


# Pagination 分页组件

一个简单易用的 React 分页组件,支持页码导航、快速跳转等功能。

<img width="259" alt="image" src="https://github.com/user-attachments/assets/10a04dbc-2f48-4c6a-af92-7f47aae9dd12" />


## 功能特点

- 支持上一页/下一页导航
- 显示当前页码状态
- 支持快速跳转到首尾页
- 页码区块化显示
- 可自定义样式

## Props

| 参数              | 说明               | 类型                   | 默认值 |
| ----------------- | ------------------ | ---------------------- | ------ |
| current           | 当前页码           | number                 | -      |
| total             | 总页数             | number                 | -      |
| onChange          | 页码改变的回调函数 | (page: number) => void | -      |
| className         | 容器类名           | string                 | -      |
| buttonCls         | 按钮类名           | string                 | -      |
| buttonDisabledCls | 按钮禁用时的类名   | string                 | -      |
| style             | 容器样式           | React.CSSProperties    | -      |

## 基础用法

```
import { Pagination } from '@kqinfo/ui';
export default () => {
const [current, setCurrent] = useState(1);
return (
<Pagination
current={current}
total={10}
onChange={(page) => setCurrent(page)}
/>
);
}
```

## 自定义样式

```
import { Pagination } from '@kqinfo/ui';
export default () => {
return (
<Pagination
current={1}
total={10}
onChange={(page) => console.log(page)}
className="custom-pagination"
buttonCls="custom-button"
buttonDisabledCls="custom-button-disabled"
style={{ margin: '20px 0' }}
/>
);
}
```

## 特性说明

1. 页码显示规则

- 默认显示5个页码
- 当前页码超出显示范围时,会显示快速前进/后退按钮
- 始终显示第一页和最后一页的页码

2. 按钮状态

- 第一页时,上一页按钮禁用
- 最后一页时,下一页按钮禁用

3. 快速跳转

- 点击 << 向前跳转5页
- 点击 >> 向后跳转5页
- 跳转不会超出总页数范围

# Table 表格

用于展示多行多列数据的表格组件。

## 引入

```
import { Table } from '@kqinfo/ui';
```

## 基础用法

```
import React from 'react';
import { Table } from '@kqinfo/ui';
interface DataType {
name: string;
age: number;
address: string;
}
const columns = [
{
title: '姓名',
dataIndex: 'name',
},
{
title: '年龄',
dataIndex: 'age',
},
{
title: '地址',
dataIndex: 'address',
},
];
const data: DataType[] = [
{
name: '张三',
age: 18,
address: '北京',
},
{
name: '李四',
age: 20,
address: '上海',
},
];
export default () => {
return <Table columns={columns} dataSource={data} />;
};
```

## API

### Props

| 参数        | 说明                       | 类型                    | 默认值            |
| ----------- | -------------------------- | ----------------------- | ----------------- |
| dataSource  | 表格数据源                 | `T[]`                   | -                 |
| columns     | 表格列的配置               | `Column<T>[]`           | -                 |
| loading     | 页面是否加载中             | `boolean`               | `false`           |
| doubleColor | 双行的高亮颜色             | `string`                | 主题色的0.1透明度 |
| align       | 文字对齐方式               | `'center' | 'between'` | -                 |
| shadow      | 阴影配置,设置为false不显示 | `false | ShadowProps`  | -                 |
| onRowTap    | 行点击事件                 | `(data: T) => void`     | -                 |
| headerCls   | 表头类名                   | `string`                | -                 |
| headerStyle | 表头样式                   | `CSSProperties`         | -                 |
| bodyCls     | 表格主体类名               | `string`                | -                 |
| bodyStyle   | 表格主体样式               | `CSSProperties`         | -                 |
| rowCls      | 行类名                     | `string`                | -                 |
| rowStyle    | 行样式                     | `CSSProperties`         | -                 |
| itemCls     | 单元格类名                 | `string`                | -                 |
| itemStyle   | 单元格样式                 | `CSSProperties`         | -                 |
| noDataCls   | 空数据组件类名             | `string`                | -                 |
| noDataStyle | 空数据组件样式             | `CSSProperties`         | -                 |

### Column

| 参数      | 说明                       | 类型                                  | 默认值 |
| --------- | -------------------------- | ------------------------------------- | ------ |
| title     | 列头显示文字               | `ReactNode`                           | -      |
| dataIndex | 列数据在数据项中对应的路径 | `keyof T`                             | -      |
| width     | 列宽度                     | `number`                              | -      |
| render    | 自定义渲染函数             | `(value, record, index) => ReactNode` | -      |

## 代码演示
<img width="314" alt="image" src="https://github.com/user-attachments/assets/281c9168-0836-4ace-adef-ea5797dcb1a6" />

### 自定义渲染

```
const columns = [
{
title: '姓名',
dataIndex: 'name',
render: (name) => <Text style={{ color: 'red' }}>{name}</Text>
}
];
```

### 设置列宽

```
const columns = [
{
title: '姓名',
dataIndex: 'name',
width: 200
}
];
```

### 开启加载状态

```
<Table loading columns={columns} dataSource={data} />
```

### 双行高亮

```
<Table doubleColor="#f5f5f5" columns={columns} dataSource={data} />
```

### 行点击事件

```
<Table
columns={columns}
dataSource={data}
onRowTap={(record) => {
console.log('点击行:', record);
}}
/>
```

# DropDownMenu 下拉菜单

可展开和收起的下拉菜单组件。

## 介绍

DropDownMenu 是一个可复用的下拉菜单组件,支持以下特性:

- 支持展开/收起下拉选项
- 可配置遮罩层
- 支持手动控制显示状态
- 支持自定义样式
- 提供显示/隐藏状态回调

## 基础用法

```
import { DropDownMenu } from '@kqinfo/ui';
export default () => {
return (
<DropDownMenu>
<DropDownMenu.Item>选项1</DropDownMenu.Item>
<DropDownMenu.Item>选项2</DropDownMenu.Item>
</DropDownMenu>
);
}
```

## API

### Props

| 参数            | 说明                   | 类型                                      | 默认值 |
| --------------- | ---------------------- | ----------------------------------------- | ------ |
| className       | 外层样式类名           | string                                    | -      |
| showModal       | 是否显示遮罩层         | boolean                                   | true   |
| children        | 子元素                 | React.ReactNode                           | -      |
| onOpsVisible    | 显示/隐藏回调函数      | (visible: boolean, index: number) => void | -      |
| opsVisibleIndex | 手动控制显示的选项索引 | number                                    | -1     |
| style           | 内联样式               | React.CSSProperties                       | -      |
| topHeight       | 定位顶部高度           | number                                    | 100    |

### onOpsVisible 回调参数

| 参数    | 说明               | 类型    |
| ------- | ------------------ | ------- |
| visible | 是否显示           | boolean |
| index   | 当前操作的选项索引 | number  |

## 注意事项

1. 组件需要配合 DropDownMenu.Item 一起使用

2. topHeight 的单位为 rpx

3. 设置 opsVisibleIndex 可以手动控制显示的选项

4. showModal 设为 false 时将不显示遮罩层

   

# DropDownMenuItem 下拉菜单项

一个可定制的下拉菜单项组件,支持选项列表、自定义样式、状态控制等功能。

<img width="321" alt="image" src="https://github.com/user-attachments/assets/7b541dfe-fadd-4035-b3bc-41b5b26cf911" />


## 基础用法

```
import { DropDownMenuItem } from '@kqinfo/ui';
export default () => {
const options = [
{ text: '选项1', value: 1 },
{ text: '选项2', value: 2 }
];
return (
<DropDownMenuItem
title="请选择"
options={options}
value={1}
onChange={(value, item) => {
console.log('selected:', value, item);
}}
/>
);
}
```

## API

### Props

| 参数          | 说明             | 类型                                                     | 默认值      |
| ------------- | ---------------- | -------------------------------------------------------- | ----------- |
| className     | 外层容器类名     | `string`                                                 | -           |
| itemCls       | 选项样式类名     | `string`                                                 | -           |
| itemSelectCls | 选中项样式类名   | `string`                                                 | -           |
| maxHeight     | 下拉面板最大高度 | `string | number`                                       | `'50vh'`    |
| value         | 当前选中值       | `any`                                                    | -           |
| title         | 显示的标题       | `string`                                                 | -           |
| options       | 选项数据         | `Array<{text: string, value: any}>`                      | -           |
| onChange      | 选择回调         | `(value: any, item: {text: string, value: any}) => void` | -           |
| icon          | 箭头图标名称     | `IconNames`                                              | `'kq-down'` |
| arrowsCls     | 箭头图标类名     | `string`                                                 | -           |
| arrowsColor   | 箭头图标颜色     | `string`                                                 | `'#bbb'`    |
| arrowsSize    | 箭头图标大小     | `number`                                                 | `28rpx`     |
| onTap         | 自定义点击事件   | `() => boolean | void`                                  | -           |
| titleCls      | 标题类名         | `string`                                                 | -           |
| dowCls        | 下拉面板类名     | `string`                                                 | -           |

### options 数据结构

```
interface Option {
text: string; // 显示文本
value: any; // 选项值
}
```

## 进阶用法

### 自定义样式

```
<DropDownMenuItem
className="custom-dropdown"
itemCls="custom-item"
itemSelectCls="custom-selected"
titleCls="custom-title"
dowCls="custom-panel"
arrowsCls="custom-arrow"
// ...
/>
```

### 自定义点击行为

```
<DropDownMenuItem
onTap={() => {
// 返回 false 可阻止展开/折叠
if (someCondition) {
return false;
}
// do something
}}
/>
```

### 自定义内容

```
<DropDownMenuItem title="自定义">
<View className="custom-content">
// 自定义下拉面板内容
</View>
</DropDownMenuItem>
```

## 注意事项

1. 在移动端使用时会自动调整定位方式为 fixed
2. maxHeight 默认为 50vh,可根据实际需求调整
3. onTap 回调返回 false 时可阻止展开/折叠动作
4. 支持通过 children 定制下拉面板的内容

## 样式定制

组件默认样式类名:

- `.down` - 下拉面板
- `.downSelect` - 选项
- `.select` - 选中状态
- `.downItem` - 触发器
- `.flexCenter` - 居中布局
- `.icon` - 箭头图标

可通过对应的 className props 覆盖这些样式。

# Tab 标签页组件

Tab 组件用于在不同视图之间切换。支持卡片式和普通两种外观,可以进行受控和非受控的使用。

<img width="317" alt="image" src="https://github.com/user-attachments/assets/a5f81909-74e9-465d-8c21-06e5fbf8c2ab" />


## 代码示例

### 基础用法

```
import { Tab } from '@kqinfo/ui';
export default () => {
const tabs = [
{ content: '标签1', index: 0 },
{ content: '标签2', index: 1 }
];
return (
<Tab
tabs={tabs}
onChange={(index) => console.log('切换到:', index)}
/>
);
};
```

### 卡片式标签页

```
import { Tab } from '@kqinfo/ui';
export default () => {
const tabs = [
{ content: '标签1', index: 0 },
{ content: '标签2', index: 1 }
];
return (
<Tab
type="card"
tabs={tabs}
onChange={(index) => console.log('切换到:', index)}
/>
);
};
```

### 受控用法

```
import { Tab } from '@kqinfo/ui';
import { useState } from 'react';
export default () => {
const [active, setActive] = useState(0);
const tabs = [
{ content: '标签1', index: 0 },
{ content: '标签2', index: 1 }
];
return (
<Tab
tabs={tabs}
current={active}
onChange={setActive}
control
/>
);
};
```

## API

### Props

| 参数          | 说明                 | 类型                                    | 默认值      |
| ------------- | -------------------- | --------------------------------------- | ----------- |
| tabs          | 标签页配置           | `Array<{content: ReactNode, index: T}>` | -           |
| current       | 当前激活的标签页索引 | `T`                                     | -           |
| onChange      | 切换标签页的回调函数 | `(index: T) => void`                    | -           |
| control       | 是否为受控组件       | `boolean`                               | `false`     |
| type          | 标签页样式类型       | `'default' | 'card'`                   | `'default'` |
| className     | 容器类名             | `string`                                | -           |
| containerCls  | 内容区域类名         | `string`                                | -           |
| itemCls       | 标签项类名           | `string`                                | -           |
| activeItemCls | 激活状态的标签项类名 | `string`                                | -           |
| style         | 容器样式             | `CSSProperties`                         | -           |

### 特性说明

1. 支持泛型类型 `T`,可以自定义 tab 的 index 类型
2. 当只有两个标签页时,会自动添加一个带动画效果的分隔线
3. 可以通过 `control` 属性切换受控/非受控模式
4. 提供了 card 类型的替代样式

### 注意事项

1. 在受控模式下,需要同时提供 `current` 和 `onChange` 属性
2. `tabs` 数组中的 `index` 值需要保持唯一
3. 样式定制可以通过 `className`、`itemCls` 等属性实现

# TabBar 标签栏

移动端底部导航标签栏组件。

<img width="316" alt="image" src="https://github.com/user-attachments/assets/58f1fa59-b881-47f5-bc8e-3ebe257fb539" />


## 介绍

TabBar 是一个用于移动端的底部导航组件,支持图标和文字的显示,可以方便地控制当前激活项,并且支持安全区域。

## 基础用法

```
import { TabBar } from '@kqinfo/ui';
import { Home, User } from '@/icons';
export default () => {
return (
<TabBar
items={[
{
title: '首页',
icon: (active) => <Home color={active ? '#1890ff' : '#999'} />,
index: 0
},
{
title: '我的',
icon: (active) => <User color={active ? '#1890ff' : '#999'} />,
index: 1
}
]}
onChange={(current) => {
console.log('当前选中:', current);
}}
/>
);
}
```

## API

### TabBar Props

| 参数        | 说明           | 类型                                | 默认值       |
| ----------- | -------------- | ----------------------------------- | ------------ |
| className   | 自定义样式名   | string                              | -            |
| style       | 行内样式       | CSSProperties                       | -            |
| color       | 文字颜色       | string                              | #bebebe      |
| activeColor | 选中后文字颜色 | string                              | brandPrimary |
| current     | 当前位置索引   | number | string                    | -            |
| items       | tabBar数据     | TabBarItemProps[]                   | []           |
| onChange    | 切换时触发     | (current: number | string) => void | -            |
| itemCls     | 子项类名       | string                              | -            |

### TabBarItemProps

| 参数  | 说明                    | 类型                                          | 默认值 |
| ----- | ----------------------- | --------------------------------------------- | ------ |
| title | tab名称                 | ReactNode                                     | -      |
| icon  | 设置图标,传null则不显示 | ReactNode | ((active: boolean) => ReactNode) | -      |
| index | 路由索引                | number | string                              | -      |
| hide  | 是否隐藏                | boolean                                       | false  |

## 注意事项

1. icon 支持两种传入方式:
   - ReactNode: 直接传入图标组件
   - Function: 传入函数,可根据激活状态返回不同样式的图标

2. 组件会自动处理安全区域,确保在全面屏设备上有正确的底部间距

3. 可以通过 hide 属性动态控制某一项是否显示

# Menu 菜单组件

一个功能丰富的多级菜单组件,支持多种展示模式和自定义样式。

## 功能特点

- 支持多级菜单结构
- 提供三种展示模式:children(默认)、list、singleCol 
- 支持二级菜单的折叠和子菜单模式
- 丰富的样式自定义
- 支持适老化模式

## 基础用法

<img width="312" alt="image" src="https://github.com/user-attachments/assets/dd27beb8-9be6-4e5a-be1f-ee99053489fc" />


```
import { Menu } from '@kqinfo/ui'
const data = [
{
id: '1',
name: '一级菜单',
children: [
{
id: '1-1',
name: '二级菜单',
children: [
{
id: '1-1-1',
name: '三级菜单'
}
]
}
]
}
]
export default () => (
<Menu
data={data}
onChange={(id, children) => {
console.log('当前选中:', id)
}}
onSelect={item => {
console.log('选中项:', item)
}}
/>
)
```

## API

### Props

| 参数             | 说明                     | 类型                                     | 默认值       |
| ---------------- | ------------------------ | ---------------------------------------- | ------------ |
| data             | 菜单数据                 | `MenuItem[]`                             | -            |
| menuMode         | 菜单模式                 | `'children' \| 'list' \| 'singleCol'`    | `'children'` |
| childrenMenuMode | 二级菜单模式             | `'collapse' \| 'subMenu'`                | `'subMenu'`  |
| current          | 当前选中的菜单id         | `string \| number`                       | 第一个可选项 |
| elderly          | 适老模式                 | `boolean`                                | `false`      |
| onChange         | 菜单切换事件             | `(id: ID, children: MenuItem[]) => void` | -            |
| onSelect         | 选择菜单项事件           | `(item: MenuItem) => void`               | -            |
| autoFlexChildren | 自动折叠右侧展开的子菜单 | `boolean`                                | `false`      |

### MenuItem 数据结构

```
interface MenuItem {
id: string | number; // 唯一标识
name: React.ReactNode; // 菜单名称
children?: MenuItem[]; // 子菜单
}
```

### 样式相关Props

| 参数                  | 说明                 | 类型     |
| --------------------- | -------------------- | -------- |
| className             | 组件容器类名         | `string` |
| leftCls               | 左侧区域类名         | `string` |
| leftItemCls           | 左侧菜单项类名       | `string` |
| leftActiveCls         | 左侧选中项类名       | `string` |
| leftChildrenActiveCls | 左侧子菜单选中项类名 | `string` |
| rightCls              | 右侧区域类名         | `string` |
| rightItemCls          | 右侧菜单项类名       | `string` |
| rightActiveCls        | 右侧选中项类名       | `string` |
| rightItemChildrenCls  | 右侧子菜单类名       | `string` |
| listCls               | list模式容器类名     | `string` |
| listItemCls           | list模式菜单项类名   | `string` |

## 不同模式示例

### children 模式 (默认)
<img width="310" alt="image" src="https://github.com/user-attachments/assets/2aa45880-f92c-4326-a3c6-9bbc6bc5a206" />

左右两栏布局,支持多级菜单。

```
<Menu
data={data}
menuMode="children"
childrenMenuMode="subMenu"
/>
```

### list 模式

单列展示所有菜单项。
<img width="310" alt="image" src="https://github.com/user-attachments/assets/a8b4d55d-5219-4543-aff6-3274c05e7190" />

```
<Menu
data={data}
menuMode="list"
/>
```

### singleCol 模式 

单列可折叠菜单。
<img width="313" alt="image" src="https://github.com/user-attachments/assets/fcfe94bf-2133-442e-bf40-eb3f8b299286" />

```
<Menu
data={data}
menuMode="singleCol"
/>
```

## 注意事项

1. data 数据中的 id 必须唯一
2. 建议根据实际场景选择合适的展示模式
3. 可以通过样式相关的 Props 进行样式自定义
4. 适老模式会增大字号和间距

# Swiper 轮播图组件

基于 Swiper 封装的 React 轮播图组件，支持自动播放、分页指示器等特性。

## 基础用法

```
import Swiper from '@kqinfo/ui';
export default () => {
const items = [
{
node: <div>Slide 1</div>
},
{
node: <div>Slide 2</div>
},
{
node: <div>Slide 3</div>
}
];
return (
<Swiper
items={items}
autoplay
indicatorDots
/>
);
}
```

## Props

| 参数                 | 说明                                 | 类型                                       | 默认值  |
| -------------------- | ------------------------------------ | ------------------------------------------ | ------- |
| items                | 轮播项数组，每项包含 node(React节点) | `Array<{node: ReactNode}>`                 | -       |
| indicatorDots        | 是否显示指示器，可选 `true`/`'line'` | `boolean \| 'line'`                        | `false` |
| lineDotsCls          | 线状指示器的自定义类名               | `string`                                   | -       |
| autoplay             | 是否自动播放                         | `boolean`                                  | `false` |
| interval             | 自动播放间隔时间(ms)                 | `number`                                   | `3000`  |
| current              | 当前页面的 index                     | `number`                                   | -       |
| displayMultipleItems | 同时显示的滑块数量                   | `number`                                   | `1`     |
| circular             | 是否循环播放                         | `boolean`                                  | `false` |
| vertical             | 滑动方向是否为纵向                   | `boolean`                                  | `false` |
| className            | 容器类名                             | `string`                                   | -       |
| style                | 容器样式                             | `CSSProperties`                            | -       |
| onChange             | 轮播切换时触发                       | `(e: {detail: {current: number}}) => void` | -       |

## 特性

- 支持自动播放
- 支持循环播放
- 支持垂直/水平方向滑动
- 支持显示多个滑块
- 支持点状/线状两种指示器样式
- 支持受控和非受控模式

## 注意事项

1. 使用 `current` 属性时组件为受控模式，需要配合 `onChange` 使用
2. `indicatorDots` 设置为 `'line'` 时显示线状指示器，可通过 `lineDotsCls` 自定义样式
3. 设置 `displayMultipleItems` 大于 1 时，可同时显示多个滑块

# SwipeAction 滑动操作

一个用于实现滑动显示操作按钮的组件。常用于列表项的快捷操作。

## 介绍

SwipeAction 组件基于 @kqinfo/ui 的 Swiper 组件封装,提供了便捷的滑动操作功能。通过左右滑动可以显示/隐藏操作区域。

<img width="308" alt="image" src="https://github.com/user-attachments/assets/662cd2dc-2c6b-4340-93be-4a153c4ef99a" />


## 基础用法

```
import { SwipeAction } from '@kqinfo/ui';
export default () => {
return (
<SwipeAction
action={
<div style={{ background: 'red', height: '100%', padding: '0 20px' }}>
删除
</div>
}
>
<div style={{ background: '#fff', padding: 20 }}>
列表项内容
</div>
</SwipeAction>
);
};
```

## API

### Props

| 参数      | 说明           | 类型                | 默认值 |
| --------- | -------------- | ------------------- | ------ |
| children  | 主内容区域     | React.ReactNode     | -      |
| action    | 操作区域内容   | React.ReactNode     | -      |
| className | 容器自定义类名 | string              | -      |
| style     | 容器自定义样式 | React.CSSProperties | -      |

## 特点

- 支持自定义主内容和操作区域
- 滑动流畅,体验良好
- 点击操作区域后自动关闭
- 可自定义样式

## 注意事项

1. action 区域建议设置背景色和高度以便于显示
2. 主内容区域建议设置背景色,避免透明

# Indexes 索引列表

类似通讯录的索引列表组件,支持按字母快速定位内容。
<img width="321" alt="image" src="https://github.com/user-attachments/assets/080b8cd5-186d-4075-8d7b-937e06b1bb7d" />

## 示例
```
import Indexes from '@kqinfo/ui';
const Demo = () => {
const list = [
{ name: '阿里', id: 1 },
{ name: '百度', id: 2 },
{ name: 'Chrome', id: 3 }
];
return (
<Indexes
list={list}
renderItem={(item) => ({
// 返回需要索引的文字
index: item.name,
// 渲染的节点内容
node: <div>{item.name}</div>
})}
/>
);
};
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| list | 列表数据 | `D[]` | - |
| renderItem | 渲染列表项,需要返回索引文字和渲染节点 | `(data: D) => { index: string; node: React.ReactNode }` | - |
| className | 容器类名 | `string` | - |
| indexCls | 索引标识的类名 | `string` | - |
| slideItemCls | 侧边项类名 | `string` | - |
| slideCls | 侧边栏类名 | `string` | - |
| indexLineCls | 索引分割线类名 | `string` | - |
| itemWrapCls | 单个索引列表盒子类名 | `string` | - |

### 功能特性

- 自动根据首字母生成拼音索引
- 支持触摸和鼠标事件
- 点击/触摸侧边栏可快速定位
- 滚动时自动更新当前索引
- 支持自定义样式

### 注意事项

1. renderItem 返回的 index 必须是字符串类型
2. 非字母开头的索引会归类到 '#' 分组
3. 索引会按字母顺序排序,# 永远在最后

## 样式定制

组件提供以下类名用于样式自定义:

- indexCls: 索引标识样式
- slideItemCls: 侧边栏项目样式  
- slideCls: 侧边栏容器样式
- indexLineCls: 索引分割线样式
- itemWrapCls: 列表项容器样式


# 表单与输入组件

# Form 表单组件

基于rc-field-form封装的表单组件,提供了验证、布局、缓存等增强功能。

## 基础用法

```
import Form from '@kqinfo/ui';
export default () => {
const [form] = Form.useForm();
return (
<Form
form={form}
onFinish={(values) => {
console.log(values);
}}
>
<Form.Item
name="username"
label="用户名"
rules={[{ required: true }]}
>
<Input />
</Form.Item>
<Form.Item
name="password"
label="密码"
rules={[{ required: true }]}
>
<Input type="password" />
</Form.Item>
<Button onTap={() => form.submit()}>
提交
</Button>
</Form>
);
}
```

## Props

### Form Props

| 参数           | 说明                                   | 类型                                       | 默认值             |
| -------------- | -------------------------------------- | ------------------------------------------ | ------------------ |
| form           | 经 Form.useForm() 创建的 form 控制实例 | FormInstance                               | -                  |
| initialValues  | 表单默认值                             | object                                     | -                  |
| onFinish       | 提交表单且数据验证成功后回调事件       | function(values)                           | -                  |
| onFinishFailed | 提交表单且数据验证失败后回调事件       | function({values, errorFields, outOfDate}) | 默认展示第一个错误 |
| card           | 是否启用卡片模式                       | boolean                                    | true               |
| cell           | 是否启用单元格模式                     | boolean                                    | false              |
| elderly        | 适老模式,开启后尺寸会变大              | boolean                                    | false              |
| autoCacheKey   | 设置后会自动缓存表单数据的key          | string                                     | -                  |
| autoClearCache | 提交后自动清空缓存                     | boolean                                    | true               |

### FormItem Props

| 参数       | 说明         | 类型          | 默认值 |
| ---------- | ------------ | ------------- | ------ |
| name       | 字段名       | string        | -      |
| label      | 标签名       | ReactNode     | -      |
| rules      | 校验规则     | Rule[]        | -      |
| readOnly   | 只读模式     | boolean       | false  |
| required   | 是否必填     | boolean       | false  |
| vertical   | 是否垂直布局 | boolean       | false  |
| labelWidth | label宽度    | number/string | -      |

## 特性说明

### 表单验证

支持的验证规则类型:

```
interface Rule {
type?: 'string' | 'number' | 'boolean' | 'array' | 'object' | 'phone' | 'idCard' | 'password';
required?: boolean;
message?: string;
min?: number;
max?: number;
pattern?: RegExp;
// ...
}
```

### 自动缓存

设置 autoCacheKey 后会自动缓存表单数据:

```
<Form autoCacheKey="form-cache">
{/ 表单项 /}
</Form>
```

### 布局模式

- card模式: 带阴影的卡片式布局
- cell模式: 类似单元格的紧凑布局
- vertical模式: label在上方的垂直布局

## API

### Form 方法

| 名称                | 说明           |
| ------------------- | -------------- |
| Form.useForm()      | 创建Form实例   |
| form.getFieldValue  | 获取单个字段值 |
| form.getFieldsValue | 获取一组字段值 |
| form.setFieldsValue | 设置一组字段值 |
| form.resetFields    | 重置表单       |
| form.submit         | 提交表单       |
| form.validate       | 验证表单       |

### Form.List

用于渲染表单数组字段:

```
<Form.List name="users">
{fields => (
<>
{fields.map(field => (
<Form.Item {...field}>
<Input />
</Form.Item>
))}
</>
)}
</Form.List>

```

# FormItem 表单项组件

FormItem 是一个灵活的表单项组件,用于构建表单中的单个输入项,支持标签、验证、错误提示等特性。

## 基础用法

```
import { Form, FormItem } from '@kqinfo/ui';
export default () => {
return (
<Form>
<FormItem
label="用户名"
name="username"
rules={[{ required: true }]}
>
<Input placeholder="请输入用户名" />
</FormItem>
</Form>
);
};
```

## API

### Props

| 参数          | 说明         | 类型               | 默认值  |
| ------------- | ------------ | ------------------ | ------- |
| label         | 标签文本     | `ReactNode`        | -       |
| name          | 字段名       | `string`           | -       |
| rules         | 校验规则     | `Rule[]`           | -       |
| required      | 是否必填     | `boolean`          | `false` |
| readOnly      | 是否只读     | `boolean`          | `false` |
| vertical      | 是否垂直布局 | `boolean`          | `false` |
| colon         | 是否显示冒号 | `boolean`          | `true`  |
| labelWidth    | 标签宽度     | `string \| number` | -       |
| labelStyle    | 标签样式     | `CSSProperties`    | -       |
| childrenStyle | 内容样式     | `CSSProperties`    | -       |
| className     | 自定义类名   | `string`           | -       |
| style         | 自定义样式   | `CSSProperties`    | -       |

### 校验规则

支持的规则类型:

```
{
required: boolean,
message: string,
type: string,
validator: (rule, value) => Promise
}
```

## 常见用法

### 必填验证

```
<FormItem
label="用户名"
name="username"
rules={[{ required: true, message: '请输入用户名' }]}
>
<Input />
</FormItem>
```

### 自定义验证

```
<FormItem
label="密码"
name="password"
rules={[
{
validator: async (rule, value) => {
if (!value || value.length < 6) {
throw new Error('密码长度不能小于6位');
}
}
}
]}
>
<Input type="password" />
</FormItem>
```

### 只读模式

```
<FormItem
label="用户名"
name="username"
readOnly
renderReadOnlyValue={(value) => ${value}}
>
<Input />
</FormItem>
```

### 垂直布局

```
<FormItem
label="描述"
name="desc"
vertical
>
<TextArea />
</FormItem>
```

### 自定义样式

```
<FormItem
label="用户名"
labelStyle={{ color: '#666' }}
childrenStyle={{ marginLeft: 20 }}
style={{ marginBottom: 24 }}
>
<Input />
</FormItem>
```

## 注意事项

1. FormItem 需要配合 Form 组件使用
2. name 属性用于表单数据收集和校验
3. 自定义校验规则时,validator 函数需要返回 Promise
4. 只读模式下可通过 renderReadOnlyValue 自定义显示内容

# InputNumber 数字输入框

支持加减的数字输入框组件。

## 介绍

InputNumber 是一个用于数字输入的组件,支持通过点击按钮或者输入来改变数值。

## 基础用法

```
import { InputNumber } from '@kqinfo/ui'
export default () => {
return (
<InputNumber
defaultValue={3}
min={0}
max={10}
onChange={value => console.log(value)}
/>
)
}
```

## API

### Props

| 参数              | 说明                     | 类型                                                         | 默认值                    |
| ----------------- | ------------------------ | ------------------------------------------------------------ | ------------------------- |
| value             | 当前值                   | `number`                                                     | -                         |
| defaultValue      | 默认值                   | `number`                                                     | `0`                       |
| min               | 最小值                   | `number`                                                     | `Number.MIN_SAFE_INTEGER` |
| max               | 最大值                   | `number`                                                     | `Number.MAX_SAFE_INTEGER` |
| step              | 每次改变步数，可以为小数 | `number`                                                     | `1`                       |
| disabled          | 是否禁用                 | `boolean`                                                    | `false`                   |
| unit              | 显示的单位               | `string`                                                     | -                         |
| onChange          | 变化时回调函数           | `(value: number) => void`                                    | -                         |
| formatValue       | 格式化显示值             | `(value: any) => string \| number`                           | -                         |
| iconColor         | 图标的默认颜色           | `string`                                                     | 主题色                    |
| disabledColor     | 禁用时图标的颜色         | `string`                                                     | `transparent`             |
| className         | 外层样式类名             | `string`                                                     | -                         |
| iconCls           | 图标样式类名             | `string`                                                     | -                         |
| numberCls         | 数字样式类名             | `string`                                                     | -                         |
| numberDisabledCls | 禁用时数字样式类名       | `string`                                                     | -                         |
| addBtn            | 自定义增加按钮           | `(data: { disabled: boolean; handleAdd: () => void }) => ReactNode` | -                         |
| subBtn            | 自定义减少按钮           | `(data: { disabled: boolean; handleSub: () => void }) => ReactNode` | -                         |

## 代码示例

### 基础用法

```
<InputNumber defaultValue={1} />
```

### 设置步长

```
<InputNumber step={0.1} />
```

### 设置范围

```
<InputNumber min={0} max={10} />
```

### 格式化展示

```
<InputNumber
defaultValue={1000}
formatValue={value => ${value}%}
/>
```

### 自定义按钮

```
<InputNumber
addBtn={({disabled, handleAdd}) => (
<button onClick={handleAdd} disabled={disabled}>
增加
</button>
)}
subBtn={({disabled, handleSub}) => (
<button onClick={handleSub} disabled={disabled}>
减少
</button>
)}
/>
```

### 设置单位

```
<InputNumber unit="kg" />
```

## 注意事项

1. value 为受控属性,设置后需要通过 onChange 更新
2. defaultValue 仅在初始化时生效
3. step 支持小数,组件会自动处理精度问题
4. 自定义按钮时需要自行处理禁用状态

# InputLicenseKeyBoard 车牌号输入键盘

## 介绍

一个用于输入车牌号的自定义键盘组件。继承了原生input的部分属性,同时提供了专门的车牌号输入键盘。

## 代码演示

### 基础用法

```
import { InputLicenseKeyBoard } from '@kqinfo/ui';
export default () => {
return (
<InputLicenseKeyBoard
placeholder="请输入车牌号"
onChange={val => console.log(val)}
/>
);
}
```

### 受控组件

```
import { InputLicenseKeyBoard } from '@kqinfo/ui';
import { useState } from 'react';
export default () => {
const [value, setValue] = useState('');
return (
<InputLicenseKeyBoard
value={value}
onChange={setValue}
placeholder="请输入车牌号"
/>
);

```

### 带清除按钮

```
import { InputLicenseKeyBoard } from '@kqinfo/ui';
export default () => {
return (
<InputLicenseKeyBoard
clearable
placeholder="请输入车牌号"
onClear={() => console.log('cleared')}
/>
```

## API

### Props

| 参数         | 说明               | 类型                      | 默认值  |
| ------------ | ------------------ | ------------------------- | ------- |
| value        | 输入值             | `string`                  | -       |
| defaultValue | 默认值             | `string`                  | `''`    |
| onChange     | 输入改变时触发     | `(value: string) => void` | -       |
| placeholder  | 提示文本           | `string`                  | -       |
| disabled     | 是否禁用           | `boolean`                 | `false` |
| clearable    | 是否可清除         | `boolean`                 | `false` |
| onClear      | 点击清除按钮时触发 | `() => void`              | -       |
| title        | 键盘标题           | `string`                  | -       |
| confirmText  | 确认按钮文字       | `string`                  | -       |
| safeArea     | 是否开启安全区适配 | `boolean`                 | -       |

### CSS 变量

| 属性                | 说明         | 默认值 |
| ------------------- | ------------ | ------ |
| --font-size         | 字体大小     | -      |
| --color             | 文字颜色     | -      |
| --placeholder-color | 占位符颜色   | -      |
| --text-align        | 文字对齐方式 | -      |

### Ref

| 方法名 | 说明       | 类型         |
| ------ | ---------- | ------------ |
| clear  | 清空输入值 | `() => void` |
| focus  | 获取焦点   | `() => void` |
| blur   | 失去焦点   | `() => void` |

## 注意事项

1. 组件默认是只读的,只能通过键盘输入
2. 键盘显示时会自动关闭原生键盘
3. 样式可以通过 CSS 变量进行自定义


# ReInput 输入框组件

基于 Remax/one 的 Input 组件封装的增强输入框组件。

## 使用示例

```
import ReInput from '@kqinfo/ui';
export default () => {
return (
<ReInput
placeholder="请输入内容"
onChange={value => console.log(value)}
/>
);
}
```

## API

### Props

| 参数        | 说明                     | 类型                    | 默认值 |
| ----------- | ------------------------ | ----------------------- | ------ |
| className   | 自定义类名               | string                  | -      |
| confirmType | 设置键盘右下角按钮的文字 | string                  | -      |
| onChange    | 输入框内容变化时的回调   | (value: string) => void | -      |

其他属性继承自 Remax/one 的 Input 组件。

### Ref 转发

组件支持通过 ref 访问内部的 input 元素。

```
import React, { useRef } from 'react';
import ReInput from '@kqinfo/ui';
export default () => {
const inputRef = useRef(null);
return <ReInput ref={inputRef} />;
}
```

## 注意事项

1. 组件使用 `forwardRef` 实现了 ref 转发功能
2. 样式上默认添加了 `styles.web` 类名
3. 通过 `useInput` hook 处理了输入相关的逻辑

## 类型定义

```
export type Props = UseInputOption;
```

完整的类型定义请参考 `useInput.ts` 文件。

#  ReTextarea

一个基于 Remax 的 Textarea 组件封装，提供了更便捷的输入处理能力。

## 介绍

`ReTextarea` 是对 Remax 原生 Textarea 组件的封装，通过 `useInput` hook 提供了统一的输入处理能力。

## 基础用法

```
import {Textarea} from '@kqinfo/ui';
export default () => {
const [value, setValue] = useState('');
return (
<Textarea
value={value}
onChange={setValue}
placeholder="请输入内容"
/>
);
}
```

## Props

组件支持所有 UseInputOption 的属性:

| 参数        | 说明                     | 类型                    | 默认值 |
| ----------- | ------------------------ | ----------------------- | ------ |
| value       | 输入框内容               | string                  | -      |
| onChange    | 输入内容变化时的回调函数 | (value: string) => void | -      |
| placeholder | 输入框占位文本           | string                  | -      |
| disabled    | 是否禁用                 | boolean                 | false  |

## 注意事项

1. 组件使用了 `forwardRef`，可以通过 ref 访问到原生 Textarea 节点
2. 所有 Remax Textarea 原生属性都可以直接传入使用

## 示例

### 使用 ref

```
import {Textarea} from '@kqinfo/ui';
export default () => {
const textareaRef = useRef(null);
useEffect(() => {
// 可以访问原生节点
console.log(textareaRef.current);
}, []);
return (
<Textarea
ref={textareaRef}
placeholder="带ref的文本域"
/>
);
}
```

### 受控组件

```
import {Textarea} from '@kqinfo/ui';
export default () => {
const [value, setValue] = useState('');
const handleChange = (val) => {
setValue(val);
};
return (
<Textarea
value={value}
onChange={handleChange}
placeholder="受控的文本域"
/>
);

```

# Picker 选择器

基于 antd-mobile 的选择器组件封装，支持级联选择、时间选择、日期选择等多种模式。

## 使用示例

### 基础选择器

```
import {Picker} from '@kqinfo/ui';
const options = [
{
label: '选项1',
value: '1',
},
{
label: '选项2',
value: '2',
}
];
export default () => {
const [value, setValue] = useState('1');
return (
<Picker
mode="selector"
data={options}
value={value}
onChange={setValue}
>
<div>点击选择</div>
</Picker>
);
}
```

### 时间选择器

```
import {Picker} from '@kqinfo/ui';
export default () => {
const [time, setTime] = useState('09:30');
return (
<Picker
mode="time"
value={time}
onChange={setTime}
start="09:00"
end="18:00"
>
<div>选择时间</div>
</Picker>
);
}
```

### 日期选择器

```
import {Picker} from '@kqinfo/ui';
export default () => {
const [date, setDate] = useState('2024-03-20');
return (
<Picker
mode="date"
value={date}
onChange={setDate}
start="2024-01-01"
end="2024-12-31"
>
<div>选择日期</div>
</Picker>
);
}
```

## API

### Props

| 参数        | 说明                                                         | 类型                                     | 默认值     |
| ----------- | ------------------------------------------------------------ | ---------------------------------------- | ---------- |
| mode        | 选择器类型,可选值: `selector` | `time` | `date` | `datetime` | `month` | string                                   | `selector` |
| value       | 选中值                                                       | string | number | (string | number)[] | -          |
| onChange    | 选择后的回调                                                 | (value: any) => void                     | -          |
| data        | 选项数据,仅在 mode="selector" 时有效                         | CascadePickerOption[]                    | -          |
| cols        | 列数,仅在 mode="selector" 时有效                             | number                                   | -          |
| start       | 起始值,时间格式为 HH:mm,日期格式为 YYYY-MM-DD                | string                                   | -          |
| end         | 结束值,时间格式为 HH:mm,日期格式为 YYYY-MM-DD                | string                                   | -          |
| disabled    | 是否禁用                                                     | boolean                                  | false      |
| childrenCls | 触发元素的类名                                               | string                                   | -          |

### CascadePickerOption

```
interface CascadePickerOption {
label: string
value: string | number
children?: CascadePickerOption[]
}
```

## 注意事项

1. 时间选择器(mode="time")的 value/onChange 值格式为 "HH:mm"
2. 日期选择器(mode="date")的 value/onChange 值格式为 "YYYY-MM-DD"
3. 日期时间选择器(mode="datetime")的 value/onChange 值格式为 "YYYY-MM-DD HH:mm"
4. 月份选择器(mode="month")的 value/onChange 值格式为 "YYYY-MM"
5. 级联选择器(mode="selector")的 value 支持单值和数组两种格式,当 cols=1 时为单值

# Jigsaw 拼图验证码组件

基于 jigsaw-captcha-js 封装的 React 拼图验证码组件。

## 功能特性

- 支持自定义验证码图片
- 可配置验证码尺寸
- 提供验证成功/失败回调
- 支持手动重置

## 使用示例

```
import {Jigsaw} from '@kqinfo/ui';
import { useRef } from 'react';
export default () => {
const jigsawRef = useRef();
return (
<Jigsaw
ref={jigsawRef}
imgs={['url1.jpg', 'url2.jpg']}
width={620}
height={310}
onSuccess={() => {
console.log('验证成功');
}}
onFail={() => {
console.log('验证失败');
}}
/>
);
}
```

## API

### Props

| 参数      | 说明             | 类型       | 默认值 |
| --------- | ---------------- | ---------- | ------ |
| width     | 验证码宽度       | number     | 620    |
| height    | 验证码高度       | number     | 310    |
| imgs      | 验证码图片数组   | string[]   | -      |
| onSuccess | 验证成功回调函数 | () => void | -      |
| onFail    | 验证失败回调函数 | () => void | -      |
| onRefresh | 刷新回调函数     | () => void | -      |

### Ref Methods

组件通过 ref 暴露以下方法:

| 方法名 | 说明       | 类型       |
| ------ | ---------- | ---------- |
| reset  | 重置验证码 | () => void |

## 注意事项

1. 组件会在验证成功后自动重置,延迟时间为 1 秒
2. 宽高单位采用 rpx,组件内部会自动转换为 px
3. imgs 数组变化时会触发重新初始化

# Switch 开关

iOS风格的开关选择器组件。

## 介绍

Switch 是一个开关选择器组件,用于在打开/关闭状态间进行切换。

## 引入

```
import { Switch } from '@kqinfo/ui';
```

## 代码演示

### 基础用法

```
import { Switch } from '@kqinfo/ui';
export default () => {
return <Switch defaultValue={true} onChange={value => console.log(value)} />;
};
```

### 受控模式

```
import { Switch } from '@kqinfo/ui';
import { useState } from 'react';
export default () => {
const [checked, setChecked] = useState(false);
return (
<Switch
value={checked}
onChange={value => setChecked(value)}
/>
);
};
```

### 自定义样式

```
import { Switch } from '@kqinfo/ui';
export default () => {
return (
<>
<Switch defaultValue={true} color="#f30" />
<Switch defaultValue={true} fontSize={40} />
</>
);
};
```

### 禁用状态

```
import { Switch } from '@kqinfo/ui';
export default () => {
return <Switch defaultValue={true} disabled />;
};
```

## API

| 参数         | 说明                          | 类型                       | 默认值  |
| ------------ | ----------------------------- | -------------------------- | ------- |
| value        | 是否选中,设置后变为受控组件   | `boolean`                  | -       |
| defaultValue | 默认是否选中                  | `boolean`                  | -       |
| disabled     | 是否禁用                      | `boolean`                  | `false` |
| onChange     | 变化时的回调函数              | `(value: boolean) => void` | -       |
| color        | 开关背景色                    | `string`                   | 主题色  |
| fontSize     | 开关大小(高度为fontSize的2倍) | `number \| string`         | `25`    |
| className    | 外层样式类名                  | `string`                   | -       |
| circleCls    | 开关圆圈的样式类名            | `string`                   | -       |
| style        | 外层样式对象                  | `CSSProperties`            | -       |

## 常见问题

### 如何修改开关的大小?

可以通过 `fontSize` 属性统一控制开关的大小比例,组件高度为 fontSize 的 2 倍。

### 如何修改开关的颜色?

可以通过 `color` 属性修改开关打开时的背景色,默认使用主题色。


# Checkbox 复选框

复选框组件,支持单选和多选场景。

## 引入

```
import { Checkbox } from '@kqinfo/ui';
```

## 代码演示

### 基础用法

```
// 基础复选框
<Checkbox>复选框</Checkbox>
// 默认选中
<Checkbox checked={true}>默认选中</Checkbox>
// 禁用状态
<Checkbox disabled>禁用状态</Checkbox>
```

### 按钮样式

```
// 按钮样式的复选框
<Checkbox type="button">按钮样式</Checkbox>
```

### 自定义样式

```
// 自定义选中颜色
<Checkbox iconColor="#ff0000">红色勾选</Checkbox>
// 圆形复选框
<Checkbox isRound>圆形复选框</Checkbox>
```

### 复选框组

```
<Checkbox.Group value={['1', '2']} onChange={(value) => console.log(value)}>
<Checkbox value="1">选项1</Checkbox>
<Checkbox value="2">选项2</Checkbox>
<Checkbox value="3">选项3</Checkbox>
</Checkbox.Group>
```

## API

### Checkbox Props

| 参数         | 说明                     | 类型                                                         | 默认值    |
| ------------ | ------------------------ | ------------------------------------------------------------ | --------- |
| checked      | 当前是否选中             | `boolean`                                                    | -         |
| value        | 复选框的值               | `string \| number`                                           | -         |
| children     | 复选框内容               | `React.ReactNode`                                            | -         |
| onChange     | 选中状态改变时的回调函数 | `(checked: boolean, e?: any, value?: string \| number) => void` | -         |
| iconColor    | 选中时的勾选图标颜色     | `string`                                                     | '#ffffff' |
| isRound      | 是否为圆形               | `boolean`                                                    | false     |
| type         | 复选框类型               | `'normal' \| 'button'`                                       | 'normal'  |
| disabled     | 是否禁用                 | `boolean`                                                    | false     |
| className    | 自定义类名               | `string`                                                     | -         |
| activeCls    | 选中时的类名             | `string`                                                     | -         |
| boxCls       | 复选框框的类名           | `string`                                                     | -         |
| boxActiveCls | 复选框选中时的类名       | `string`                                                     | -         |

### Checkbox.Group Props

| 参数     | 说明                   | 类型                                     | 默认值 |
| -------- | ---------------------- | ---------------------------------------- | ------ |
| value    | 当前选中的值           | `(string \| number)[]`                   | []     |
| disabled | 是否禁用               | `boolean`                                | false  |
| onChange | 选中值改变时的回调函数 | `(value?: (string \| number)[]) => void` | -      |

## 注意事项

1. Checkbox.Group 中的 Checkbox value 属性必须唯一
2. 使用 Checkbox.Group 时,单个 Checkbox 的 onChange 会被 Group 接管
3. type="button" 时会显示为按钮样式,没有勾选图标

# Rate 评分

评分组件,支持自定义评分样式。

## 何时使用

- 对评价进行展示
- 对事物进行快速的评级操作

## 基础用法

```
import { Rate } from '@kqinfo/ui'
export default () => (
<>
{/ 基础用法 /}
<Rate defaultValue={3} />
{/ 自定义颜色 /}
<Rate defaultValue={3} activeColor="red" defaultColor="#eee" />
{/ 自定义大小和间距 /}
<Rate defaultValue={3} size={30} gutter="10px" />
{/ 禁用状态 /}
<Rate value={3} disabled />
</>
)
```

## API

| 参数         | 说明                   | 类型                                         | 默认值        |
| ------------ | ---------------------- | -------------------------------------------- | ------------- |
| value        | 当前评分值             | `number`                                     | -             |
| defaultValue | 默认评分值             | `number`                                     | 0             |
| disabled     | 是否禁用               | `boolean`                                    | false         |
| gutter       | 图标间距               | `string`                                     | '0.4em'       |
| size         | 图标大小               | `string \| number`                           | -             |
| onChange     | 评分改变时的回调       | `(value: number) => void`                    | -             |
| iconName     | 评分图标名称           | `IconFontNames`                              | 'kq-xingxing' |
| maxValue     | 最大评分值             | `number`                                     | 5             |
| activeColor  | 选中时的颜色           | `string`                                     | 主题色        |
| defaultColor | 未选中时的颜色         | `string`                                     | '#ccc'        |
| renderItem   | 自定义评分项的渲染方法 | `(params: RenderItemParams) => ReactElement` | -             |

### RenderItemParams

| 参数     | 说明                  | 类型      |
| -------- | --------------------- | --------- |
| actived  | 当前是否选中          | `boolean` |
| index    | 当前项的索引(从0开始) | `number`  |
| maxValue | 最大评分值            | `number`  |

## 自定义渲染

可以通过 `renderItem` 自定义评分项的渲染内容:

```
import { Rate } from '@kqinfo/ui'
export default () => (
<Rate
defaultValue={3}
renderItem={({ actived, index }) => (
<View
style={{
width: 20,
height: 20,
backgroundColor: actived ? 'gold' : '#eee',
borderRadius: '50%'
}}
/>
)}
/>
)
```

