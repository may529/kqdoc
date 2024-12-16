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

## 布局组件

### Space

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


## 背景图组件

### BackgroundImage 

#### 一般用法

效果图：

<img width="346" alt="image" src="https://github.com/user-attachments/assets/38dd7000-8e03-429d-aecd-d0fd1e6c00d2" />



```
<BackgroundImg
        img={bg}
        className={styles.topBackground}
        imgProps={{
          style: { width: '100%', height: '100%' },
        }}>
        <Space className={styles.topbox} size={20}>
          <Image src={avtor} className={styles.avtor} />
          <Space flex={1} vertical size={20}>
            <Space className={styles.name}>
              王嘉琪
            </Space>
            <Space className={styles.phone}>
              138****9966
            </Space>
          </Space>
         </Space>
</BackgroundImg>
```

#### API
| 属性名         | 描述            | 类型            | 默认值 |
| :------------- | :-------------- | :-------------- | :----- |
| imgProps       | 图片的props     | `ImageProps`    | `-`    |
| img            | 背景图          | `string`        | `-`    |
| innerProps     | 里层view的props | `ViewProps`     | `-`    |
| isPreviewImage | -               | `boolean`       | `-`    |
| className      | 样式名               | `string`        | `-`    |
| style          | 行内样式              | `CSSProperties` | `-`    |


## 图片组件

### Image 

#### 一般用法

效果图：

<img width="95" alt="image" src="https://github.com/user-attachments/assets/f992690e-ca7c-40b3-81b5-3304d9f8756d" />




```
<Image src={CommonImg.doctor} style={{ width: 100, height: 100 }} />
  
```
#### 默认占位图

效果图：

<img width="87" alt="image" src="https://github.com/user-attachments/assets/198e78a4-8277-4742-9fca-37e754ce0cb1" />



```
<Image style={{ width: 100, height: 100 }} />
  
```

#### API

| 属性名      | 描述                       | 类型                                                         | 默认值 |
| :---------- | :------------------------- | :----------------------------------------------------------- | :----- |
| placeholder | 占位图片                   | `string | false`                                             | `-`    |
| preview     | 支持预览                   | `boolean`                                                    | `true` |
| lazyLoad    | 图片懒加载，只在小程序有效 | `boolean`                                                    | `-`    |
| onLoad      | 当图片载入完毕时触发       | `(e: Event) => void`                                         | `-`    |
| onError     | 当错误发生时触发           | `(e: Event) => void`                                         | `-`    |
| className   | 样式名                          | `string`                                                     | `-`    |
| style       | 行内样式                          | `CSSProperties`                                              | `-`    |
| src         | 图片资源地址               | `string`                                                     | `-`    |
| mode        | 图片裁剪、缩放的模式       | `"scaleToFill" | "aspectFit" | "aspectFill" | "widthFix" | "top" | "bottom" | "center" | "left" | "right" | "top left" | "top right" | "bottom left" | "bottom right"` | `-`    |



## 条形码组件

### BarCode 

#### 一般用法

效果图：

<img width="162" alt="image" src="https://github.com/user-attachments/assets/b9245f35-94b8-41da-9d0e-658f0775a057" />



```
<BarCode content={'233'} style={{ width: 200, height: 200 }} />
  
```

#### API

| 属性名    | 描述       | 类型            | 默认值   |
| :-------- | :--------- | :-------------- | :------- |
| content   | 条形码内容 | `string`        | `(必选)` |
| width     | 条码宽度   | `number`        | `-`      |
| height    | 条码高度   | `number`        | `-`      |
| webProps  | -          | `any`           | `-`      |
| className | 样式名     | `string`        | `-`      |
| style     | 行内样式   | `CSSProperties` | `-`      |


## 二维码组件

### QrCode

#### 一般用法

效果图：

<img width="167" alt="image" src="https://github.com/user-attachments/assets/45795892-3336-4305-8206-a5e347f38566" />



```
<QrCode
        content={'233'}
        style={{ width: 200, height: 200 }}
        showModal
        modalTitle={'二维码弹窗'}
      />
  
```

#### API

| 属性名      | 描述                 | 类型                                                         | 默认值   |
| :---------- | :------------------- | :----------------------------------------------------------- | :------- |
| content     | 二维码内容           | `string`                                                     | `(必选)` |
| darkColor   | 二维码码的颜色       | `string`                                                     | `-`      |
| lightColor  | 二维码背景颜色       | `string`                                                     | `-`      |
| onSetSrc    | 设置二维码回调       | `(src: string) => void`                                      | `-`      |
| longTapSave | 长按保存             | `boolean`                                                    | `-`      |
| showModal   | 点击显示弹窗         | `boolean`                                                    | `-`      |
| modalTitle  | 弹窗标题             | `ReactNode`                                                  | `-`      |
| onLoad      | 当图片载入完毕时触发 | `(e: Event) => void`                                         | `-`      |
| onError     | 当错误发生时触发     | `(e: Event) => void`                                         | `-`      |
| className   | -                    | `string`                                                     | `-`      |
| style       | -                    | `CSSProperties`                                              | `-`      |
| src         | 图片资源地址         | `string`                                                     | `-`      |
| mode        | 图片裁剪、缩放的模式 | `"scaleToFill" | "aspectFit" | "aspectFill" | "widthFix" | "top" | "bottom" | "center" | "left" | "right" | "top left" | "top right" | "bottom left" | "bottom right"` | `-`      |
| ref         | -                    | `Ref<unknown>`                                               | `-`      |
| key         | -                    | `Key`                                                        | `-`      |



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

