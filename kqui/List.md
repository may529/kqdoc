---
nav:
  title: 组件
  path: /components
group:
  title: 数据展示
  path: /data-display
---

## List 懒加载列表

用于在滚动到底部时自动加载下一页数据的懒加载列表组件，支持错误重试、空占位、加载提示、刷新列表、虚拟滚动（需提供每项高度）以及配合 Space 布局。

### 何时使用

- 列表数据较多，需要分批加载并在滚动到底部自动继续加载；
- 需要在加载失败时提供重试入口；
- 需要在没有数据或已经加载到末尾时展示提示；
- 需要在超长列表中优化渲染性能（提供每项高度以开启虚拟滚动）。

```tsx
import React, { useCallback, useState, useRef } from 'react';
import { Space, List, Search, Button } from '@kqinfo/ui';
import getList from '../_mock/getList';

export default () => {
  const [search, setSearch] = useState();
  const listRef = useRef<{
    refreshList: (retainList?: boolean) => Promise<void>;
  }>(null);
  return (
    <Space vertical size={'10px'}>
      <Space size={'10px'}>
        <Button onTap={() => listRef.current?.refreshList()}>完全刷新</Button>
        <Button onTap={() => listRef.current?.refreshList(true)}>
          保留列表刷新
        </Button>
      </Space>
      <Search showBtn onConfirm={v => setSearch(v)} />
      <List
        ref={listRef}
        defaultLimit={100}
        // getList要用useCallback包一下，不然会出现重复请求
        getList={useCallback(
          (page, limit) => {
            return getList(page, limit, 1, search);
            // useCallback的依赖项可以放请求列表的参数，参数变了会自动刷新列表
          },
          [search],
        )}
        renderItem={({ random, id, search }) => (
          <div key={id}>
            random: {random} id: {id} search：{search}
          </div>
        )}
      />
    </Space>
  );
};
```

### 虚拟滚动（提供每项高度）

当列表项渲染固定且可预估高度时，可传入 `renderItemHeight`（单位为 rpx 的数字），组件将按页进行可视渲染，显著提升长列表性能。

```tsx
import React, { useCallback } from 'react';
import { List } from '@kqinfo/ui';
import getList from '../_mock/getList';

export default () => (
  <List
    defaultLimit={50}
    getList={useCallback((page, limit) => getList(page, limit, 1), [])}
    renderItemHeight={() => 120 /* rpx */}
    renderItem={({ id }) => (
      <div key={id} style={{ height: 60 }}>
        Item: {id}
      </div>
    )}
  />
);
```

### 自定义占位与布局

- 可通过 `noData` 和 `noMore` 定制空占位与“已到底”提示；
- 通过 `loadingTip` 定制加载提示；
- 通过 `space` 在外层使用 Space 布局（仅当传入时生效）。

```tsx
import React, { useCallback } from 'react';
import { List } from '@kqinfo/ui';

export default () => (
  <List
    space={{ vertical: true, size: '8px' }}
    noData={<div style={{ color: '#999' }}>暂无数据</div>}
    noMore={<div style={{ color: '#999' }}>已经到底啦～</div>}
    loadingTip={<div style={{ color: '#999' }}>加载中...</div>}
    defaultLimit={20}
    getList={useCallback(async (page, limit) => {
      // 返回接口数据
      return {
        list: Array.from({ length: limit }).map((_, i) => ({
          id: page * 100 + i,
        })),
        isEnd: page > 5,
      };
    }, [])}
    renderItem={({ id }) => <div key={id}>Item: {id}</div>}
  />
);
```

### 说明

- 列表底部通过 `Visible` 组件监听可见性，当底部进入视口时触发下一页加载；
- `ref` 暴露 `refreshList(retainList?: boolean)`：
  - `refreshList()` 完全刷新（清空列表并重新加载）；
  - `refreshList(true)` 保留已有列表，仅重拉数据；
- `defaultLimit` 控制分页大小（默认 10）；
- `noData` 默认值为 `<NoData/>`；`loadingTip` 默认值为 `<Loading type={'inline'}/>`；
- 开启虚拟滚动需传入 `renderItemHeight`（返回 rpx 的数值），并确保实际渲染的高度与该值匹配；
- 建议使用 `useCallback` 包裹 `getList`，并将依赖项设置为请求参数，以避免重复请求和确保在参数变化时自动刷新列表。

### API

<API src="./index.tsx"></API>
