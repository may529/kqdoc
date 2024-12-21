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

