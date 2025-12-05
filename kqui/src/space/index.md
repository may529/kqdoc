---
nav:
  title: 组件
  path: /components
group:
  title: 布局
  path: /layout
---

## Space 布局分割

用于在横向或纵向排列子元素并设置统一间距的布局组件。支持对齐、分布、换行、容器内外间距与网格场景。若未生效，请确保子元素支持 `style` 属性。

### 何时使用

- 在列表、按钮组、卡片内容等需要均匀分隔的场景；
- 需要快速构建横向/纵向的弹性布局；
- 需要在网格/换行场景中控制某些位置不设间距（如每行最后一个）。

```tsx
import React from 'react';
import { Button, Space, PartTitle } from '@kqinfo/ui';

export default () => (
  <Space vertical size={'10px'}>
    <PartTitle>横排分割</PartTitle>
    <Space size={'10px'}>
      <Button block={false}>1</Button>
      <Button>2</Button>
      <Button type={'primary'}>3</Button>
    </Space>
    <PartTitle>竖排分割</PartTitle>
    <Space vertical size={'10px'} alignItems={'flex-start'}>
      <Button block={false}>1</Button>
      <Button>2</Button>
      <Button type={'primary'}>3</Button>
    </Space>
    <PartTitle>对齐与分布</PartTitle>
    <Space
      size={'10px'}
      alignItems={'center'}
      justify={'space-between'}
      style={{ background: '#fff' }}
    >
      <Button block={false}>A</Button>
      <Button block={false}>B</Button>
      <Button block={false}>C</Button>
    </Space>
    <PartTitle>构建列表子项布局</PartTitle>
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
    <PartTitle>容器内外间距</PartTitle>
    <Space size={8} margin={20} padding={10} style={{ background: '#fff' }}>
      <Button block={false}>Left</Button>
      <Button block={false}>Right</Button>
    </Space>
    <PartTitle>网格布局</PartTitle>
    <Space ignoreNum={4} flexWrap={'wrap'} size={'14px'}>
      {new Array(6).fill(0).map((_, i) => (
        <Space
          vertical
          style={{ width: '21%' }}
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
  </Space>
);
```

### 使用说明

- `size` 支持 `number` 或 `string`：`number` 将按 rpx 转换为像素；`string` 可传 `px`、`em` 等自定义单位；
- `vertical` 切换为纵向排列；`justify` 控制主轴分布；`alignItems` 控制交叉轴对齐；
- `flex/flexWrap` 可用于构建自适应网格；`ignoreNum` 在一行的第 N 个位置不设置间距；
- 组件本身支持 `margin`/`padding` 作为容器内外间距；
- 子元素需支持 `style` 才能应用间距；若传入非 React 节点，会自动包裹为 `View`。

<API src="./index.tsx" exports='["default","Props"]'></API>
