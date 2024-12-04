# actionConfirm

## 操作确认

通常用在表格操作

效果图

![image-20241204222728428](/Users/majirong/Library/Application Support/typora-user-images/image-20241204222728428.png)

```
import React from 'react';
import { Button } from 'antd';
import { actionConfirm } from 'parsec-admin';

export default () => (
  return (
    <Button
        type={'primary'}
        onClick={() => actionConfirm(async () => {
          // await 删除接口
         return useApi.del.request({
                        id: '1'
                      })
        }, '删除')}
      >
        删除
     </Button>
  );
);
```

# ActionsWrap

## 操作项

通常跟 [LinkButton](https://kanban.cqkqinfo.com/docs/kaiqiao-admin/components/link-button) 使用，会对多个 button 用分割线隔开。

### 基本用法

效果图

![image-20241204223751253](/Users/majirong/Library/Application Support/typora-user-images/image-20241204223751253.png)

```
import React from 'react';
import { LinkButton, ActionsWrap } from 'parsec-admin';

export default () => (
  <ActionsWrap>
    <LinkButton>编辑</LinkButton>
    <LinkButton>详情</LinkButton>
    <LinkButton>删除</LinkButton>
  </ActionsWrap>
);
```

### 多个操作项

当大于 4 个操作项时，多余的会被隐藏。可以自定义超过 2 个时隐藏。配置组件的 max 属性为 2 即可

效果图

![image-20241204224318175](/Users/majirong/Library/Application Support/typora-user-images/image-20241204224318175.png)

```
import React from 'react';
import { LinkButton, ActionsWrap } from 'parsec-admin';

export default () => (
  <ActionsWrap>
    <LinkButton>编辑</LinkButton>
    <LinkButton>详情</LinkButton>
    <LinkButton>删除</LinkButton>
    <LinkButton>选择</LinkButton>
  </ActionsWrap>
);
```

### API

| 属性     | 说明                       | 默认值 |
| -------- | -------------------------- | ------ |
| max      | 最多显示几个操作项。       | 3      |
| children | 被包含的子项，至少是两个。 | -      |



# ArrSelect

## 数组选择器

根据 Options 方便地使用 Select 组件。

### 基本用法

options可以接受多种形式

数组：[1, 2, 3]

对象：{ 1: '已启用', 2: '未启用' }

特定对象：

[
        { children: '小明', value: 'XiaoMing' },
        { children: '小红', value: 'XiaoHong' },
 ]

效果图

![image-20241204225003937](/Users/majirong/Library/Application Support/typora-user-images/image-20241204225003937.png)

```
import React from 'react';
import { ArrSelect } from 'parsec-admin';
import { Space } from 'antd';

export default () => (
  <Space>
    <ArrSelect options={[1, 2, 3]} /> //接受数组
    <ArrSelect options={{ 1: '已启用', 2: '未启用' }} /> //接受对象
    <ArrSelect
      options={[
        { children: '小明', value: 'XiaoMing' },
        { children: '小红', value: 'XiaoHong' },
      ]}
    /> //接受特定对象
  </Space>
);
```

### API

| 属性     | 说明                   | 默认值 |
| -------- | ---------------------- | ------ |
| options  | 渲染的选项。           | -      |
| arrValue | 是否返回数组形式的值。 | -      |

> 更多 API 请查看 [Select](https://ant.design/components/select-cn/#API)



# CheckboxGroup

## 多选框

根据 Options 可以创建一个 CheckboxGroup。

### 基本用法

效果图

![image-20241205034711795](/Users/majirong/Library/Application Support/typora-user-images/image-20241205034711795.png)

```
import React from 'react';
import { CheckboxGroup, Form } from 'parsec-admin';

export default () => (
  <Form
    items={[
      {
        label: '多选框',
        name: 'check',
        required: true,
        render: (
          <CheckboxGroup
            options={[
              { label: 1, value: 1 },
              { label: 2, value: 2 },
            ]}
          />
        ),
      },
    ]}
  />
);
```

### API

| 属性     | 说明                             | 默认值  |
| -------- | -------------------------------- | ------- |
| options  | 需要渲染的 Checkbox 数组。       | -       |
| objValue | 是否需要转成 `Object` 类型的值。 | `false` |



# DateShow

## 日期显示

格式化显示日期。

### 基本用法

效果图

![image-20241205034924463](/Users/majirong/Library/Application Support/typora-user-images/image-20241205034924463.png)

```
import React from 'react';
import { DateShow } from 'parsec-admin';

export default () => <DateShow>{new Date()}</DateShow>;
```

### API

| 属性     | 说明                        | 默认值 |
| -------- | --------------------------- | ------ |
| children | 需要格式化显示的 children。 | -      |



# DayPicker

## 日期选择器

选择的日期会格式化到选择日期的 0 时 0 分 0 秒，常用在搜索项。

### 基本用法

效果图

![image-20241205035144499](/Users/majirong/Library/Application Support/typora-user-images/image-20241205035144499.png)

```
import React, { useState } from 'react';
import { DayPicker} from 'parsec-admin';
import { Moment } from 'moment';

export default () => {
  const [value, setValue] = useState<Moment>();
  return (
    <>
      <DayPicker onChange={setValue} />
    </>
  );
};
```

传入值之前可以不转为 `moment` 对象。

```
import React from 'react';
import { DayPicker } from 'parsec-admin';

export default () => {
  return <DayPicker value={'2020-5-20'} />;
};
```



### API

| 属性        | 说明                | 默认值 |
| ----------- | ------------------- | ------ |
| stringValue | 将值转成ISO字符串。 | -      |
| valueFormat | 将值转为什么格式。  | -      |

> 更多参考 [DatePicker](https://ant.design/components/date-picker-cn/#API) 。



# DayRangePicker

## 日期范围选择器

 选择的日期范围会格式化到开始日期的 0 时 0 分 0 秒和结束日期的 23 时 59 分 59 秒，常用在搜索项。

### 基本用法

效果图

![image-20241205042618331](/Users/majirong/Library/Application Support/typora-user-images/image-20241205042618331.png)

```
import React, { useState } from 'react';
import { DayRangePicker } from 'parsec-admin';
import { Moment } from 'moment';

export default () => {
  const [value = [], setValue] = useState<Moment>();
  return (
      <DayRangePicker valueFormat={'YYYY-MM-DD HH:mm:ss'} onChange={setValue} />
  );
};
```

传入值之前可以不转为 `moment` 对象。

![image-20241205042738560](/Users/majirong/Library/Application Support/typora-user-images/image-20241205042738560.png)

```
import React from 'react';
import { DayRangePicker } from 'parsec-admin';

export default () => {
  return <DayRangePicker value={['2020-5-20', '2020-5-21']} />;
};
```



### API

| 属性        | 说明                | 默认值 |
| ----------- | ------------------- | ------ |
| valueFormat | 将值转为什么格式。  | -      |
| stringValue | 将值转成ISO字符串。 | -      |

> 更多用法参考 [DatePicker](https://ant.design/components/date-picker-cn/#DatePicker) 。



# Editor

## 富文本编辑器

可以像 Input 一样在 formItem 里使用的富文本编辑器。

效果图

![image-20241205045138365](/Users/majirong/Library/Application Support/typora-user-images/image-20241205045138365.png)

```tsx
import React from 'react';
import { Editor } from 'parsec-admin';
import { Form, Button } from 'antd';

export default () => (
  <Form>
    <Form.Item
      name={'text'}
      rules={[{ required: true, message: '内容是必填的' }]}
    >
      <Editor />
    </Form.Item>
    <Form.Item>
      <Button type={'primary'} htmlType={'submit'}>
        提交
      </Button>
    </Form.Item>
  </Form>
);
```

### 自定义配置

效果图

![image-20241205045205740](/Users/majirong/Library/Application Support/typora-user-images/image-20241205045205740.png)

```tsx
import React from 'react';
import { Editor } from 'parsec-admin';
import { Form, Button } from 'antd';

export default () => (
  <Form>
    <Form.Item
      name={'text'}
      rules={[{ required: true, message: '内容是必填的' }]}
    >
      <Editor
        customConfig={{ menus: ['head', 'bold', 'italic', 'underline'] }}
      />
    </Form.Item>
    <Form.Item>
      <Button type={'primary'} htmlType={'submit'}>
        提交
      </Button>
    </Form.Item>
  </Form>
);
```

### API

> 在 App 里配置了 uploadFn 后可以实现上传。

| 属性         | 说明                                                         | 默认值 |
| ------------ | ------------------------------------------------------------ | ------ |
| customConfig | 可以根据[文档](https://www.kancloud.cn/wangfupeng/wangeditor3/332599)自定义配置。 | -      |



# FixedFormActions

## 页尾操作栏

在 [高级表单](https://preview.pro.ant.design/form/advanced-form) 中，操作项过多，提交按钮就适合放在页尾。

效果图

![image-20241205051709772](/Users/majirong/Library/Application Support/typora-user-images/image-20241205051709772.png)

```tsx
import React from 'react';
import { FixedFormActions, Form } from 'parsec-admin';
import { Button, Space } from 'antd';

export default () => {
  const [form] = Form.useForm();
  return (
    <>
      <Form
        form={form}
        submitButton={false}
        items={[
          {
            label: '姓名',
            name: 'name',
            required: true,
            formItemProps: {
              extra: '提交按钮在页面最下面',
            },
          },
        ]}
      />
      <FixedFormActions>
        <Space>
          <Button onClick={() => form.resetFields()}>重置</Button>
          <Button type={'primary'} onClick={() => form.validateFields()}>
            提交
          </Button>
        </Space>
      </FixedFormActions>
    </>
  );
};
```

### API

| 属性     | 说明   | 默认值 |
| -------- | ------ | ------ |
| children | 子项。 | -      |



# form

## 表单

更加易用、美观，不需要自己布局的表单，默认布局为 [基础表单](https://preview.pro.ant.design/form/basic-form) 样式。

效果图

![image-20241205052606445](/Users/majirong/Library/Application Support/typora-user-images/image-20241205052606445.png)

```tsx
import React from 'react';
import { Form, DayRangePicker, InlineFormItemWrap } from 'parsec-admin';
import { Input, InputNumber, Radio, Button, Divider } from 'antd';

const { TextArea } = Input;
const { Item: FormItem } = Form;

export default () => (
  <Form
    autoCacheKey={'formDemo'}
    onSubmit={values =>
      new Promise(resolve => {
        console.log(values);
        setTimeout(resolve, 1000);
      })
    }
    extraButton={({ resetFields }) => (
      <Button onClick={() => resetFields()}>重置</Button>
    )}
    items={[
      {
        label: '标题',
        name: 'title',
        render: <Input placeholder={'给目标起个名字'} />,
        required: true,
      },
      {
        label: '起止日期',
        name: 'date',
        render: <DayRangePicker />,
        required: true,
      },
      {
        label: '目标描述',
        name: 'describe',
        render: <TextArea rows={4} placeholder={'请输入你的阶段性工作目标'} />,
        required: true,
      },
      {
        label: '衡量标准',
        name: 'standard',
        render: <TextArea rows={4} placeholder={'请输入衡量标准'} />,
        required: true,
      },
      () => <Divider>可以穿插各种元素</Divider>,
      {
        label: '客户',
        name: 'client',
        render: (
          <Input placeholder={'请描述你服务的客户，内部客户直接 @姓名／工号'} />
        ),
      },
      {
        label: '邀评人',
        name: 'reviewer',
        render: <Input placeholder={'请直接 @姓名／工号，最多可邀请 5 人'} />,
      },
      {
        label: '权重',
        required: true,
        render: (
          <InlineFormItemWrap>
            <FormItem
              name={'weight'}
              rules={[{ required: true, message: '权重是必填的' }]}
            >
              <InputNumber placeholder={'请输入'} />
            </FormItem>
            <span>%</span>
          </InlineFormItemWrap>
        ),
      },
      {
        label: '目标公开',
        name: 'target',
        required: true,
        render: (
          <Radio.Group
            options={[
              { label: '公开', value: 'publicity' },
              { label: '部分公开', value: 'partlyPublic' },
              { label: '不公开', value: 'private' },
            ]}
          />
        ),
        formItemProps: {
          extra: '客户、邀评人默认被分享',
        },
      },
    ]}
  />
);
```

### 表单联动

效果图

![image-20241205052640480](/Users/majirong/Library/Application Support/typora-user-images/image-20241205052640480.png)

```tsx
import React from 'react';
import { Form } from 'parsec-admin';
import { Switch, InputNumber } from 'antd';

export default () => {
  return (
    <Form
      items={[
        {
          label: '显示输入',
          name: 'show',
          formItemProps: {
            valuePropName: 'checked',
            initialValue: false,
          },
          render: <Switch />,
        },
        ({ show }) => ({
          label: '姓名',
          name: 'name',
          render: show && undefined,
        }),
        ({ show, name = '' }) => ({
          label: `${name}年龄`,
          name: 'age',
          render: show && <InputNumber />,
        }),
      ]}
    />
  );
};
```

### 表单布局

效果图

![image-20241205052659581](/Users/majirong/Library/Application Support/typora-user-images/image-20241205052659581.png)

```tsx
import React from 'react';
import { Form } from 'parsec-admin';
import { Switch, InputNumber } from 'antd';

export default () => {
  return (
    <Form
      layout={'inline'}
      formProps={{requiredMark: true}}
      items={[
        {
          label: '姓名',
          name: 'name',
          required: true
        },
        {
          label: `年龄`,
          name: 'age',
          required: true,
          render: <InputNumber />,
        },
      ]}
    />
  );
};
```

### API

| 属性         | 说明                                                         | 默认值              |
| ------------ | ------------------------------------------------------------ | ------------------- |
| form         | 自定义 form 实例。                                           | `form.useForm()[0]` |
| layout       | 自定义布局，设置为 `false` 则不布局，具体可以参考 antd form [props](https://ant.design/components/form-cn/#Form) 的 `labelCol`、`wrapperCol`字段。 | -                   |
| onSubmit     | 提交事件，当 form 检验完后会触发这个事件，需要返回一个 Promise 方法。 | -                   |
| items        | 表单项。                                                     | -                   |
| submitButton | 提交按钮，设为 `false` 则不显示。                            | `React.ReactNode`   |
| formProps    | antd form 的 [props](https://ant.design/components/form-cn/#Form) 。 | -                   |
| hideOptional | 如果不需要 label 上的'选填'的话，可以设置为 `true` 隐藏它    | `false`             |
| children     | children 会放在表单之下，提交按钮之上的地方。                | -                   |
| extraButtons | 除了提交按钮，额外的按钮。                                   | -                   |
| autoCacheKey | 自动缓存表单数据，未提交之前结束页面后再进入将回填数据。     | -                   |



# FormDescriptions

## 表述表单

可以展示详情，也可以展示为表单来提交，一般用在可编辑的详情页，样式来自 [高级表单](https://preview.pro.ant.design/form/advanced-form)

效果图

![image-20241205053032553](/Users/majirong/Library/Application Support/typora-user-images/image-20241205053032553.png)

```tsx
/**
 * background: '#f6f7f9'
 */
import React, { useState } from 'react';
import {
  FormDescriptions,
  CardLayout,
  ArrSelect,
  DayRangePicker,
  DateShow,
  Form,
} from 'parsec-admin';
import { Input, Button } from 'antd';
import moment from 'moment';

export default () => {
  const [isEdit, setIsEdit] = useState(true);
  const [data, setData] = useState({
    name: '仓库名',
    domainName: '仓库域名',
    controller: '小吴',
    approver: '小红',
    type: '私密',
  });
  const [form] = Form.useForm();
  return (
    <CardLayout
      title={'仓库管理'}
      extra={
        isEdit ? (
          <Button
            onClick={() =>
              form
                .validateFields()
                .then(values => setData(values))
                .then(() => setIsEdit(false))
            }
          >
            保存
          </Button>
        ) : (
          <Button type={'primary'} onClick={() => setIsEdit(true)}>
            编辑
          </Button>
        )
      }
    >
      <FormDescriptions
        data={data}
        edit={isEdit}
        form={form}
        items={[
          {
            label: '仓库名',
            name: 'name',
            required: true,
            formItemProps: {
              render: <Input placeholder={'请输入仓库名称'} />,
            },
          },
          {
            label: '仓库域名',
            name: 'domainName',
            required: true,
            formItemProps: {
              render: (
                <Input
                  placeholder={'请输入'}
                  addonBefore="http://"
                  addonAfter=".com"
                />
              ),
            },
          },
          {
            label: '仓库管理员',
            name: 'controller',
            required: true,
            formItemProps: {
              render: (
                <ArrSelect
                  options={['小吴', '小红']}
                  placeholder={'请选择仓库管理员'}
                />
              ),
            },
          },
          {
            label: '审批人',
            name: 'approver',
            required: true,
            formItemProps: {
              render: (
                <ArrSelect
                  options={['小吴', '小红']}
                  placeholder={'请选择审批人'}
                />
              ),
            },
          },
          {
            label: '生效日期',
            name: ['startAt', 'endAt'],
            required: true,
            formItemProps: {
              render: <DayRangePicker />,
            },
            render: ([date1, date2] = []) => (
              <>
                <DateShow>{date1}</DateShow> - <DateShow>{date2}</DateShow>
              </>
            ),
          },
          {
            label: '仓库类型',
            name: 'type',
            required: true,
            formItemProps: {
              render: (
                <ArrSelect
                  options={['私密', '公开']}
                  placeholder={'请选择仓库类型'}
                />
              ),
            },
          },
        ]}
      />
    </CardLayout>
  );
};
```

### 表单联动

效果图

![image-20241205053057980](/Users/majirong/Library/Application Support/typora-user-images/image-20241205053057980.png)

```tsx
import React from 'react';
import { FormDescriptions } from 'parsec-admin';
import { Switch } from 'antd';

export default () => {
  return (
    <FormDescriptions
      edit
      items={[
        {
          label: '显示input',
          name: 'show',
          valuePropName: 'checked',
          initialValue: false,
          formItemProps: {
            render: <Switch />,
          },
        },
        [({ show }) => ({
          label: '输入框',
          name: 'value',
          hidden: !show,
          /**
           * 传入使用了values里的什么字段可以优化性能
           */
        }), ['show']],
      ]}
    />
  );
};
```

### API

| 属性         | 说明                                                     | 默认值              |
| ------------ | -------------------------------------------------------- | ------------------- |
| form         | 自定义 form 实例。设为 `false` 可以不渲染 form 。        | `form.useForm()[0]` |
| items        | 描述项。                                                 | -                   |
| edit         | 是否可编辑。                                             | `false`             |
| loading      | 是否是加载中。                                           | `false`             |
| data         | 需要显示的详情数据。                                     | -                   |
| autoCacheKey | 自动缓存表单数据，未提交之前结束页面后再进入将回填数据。 | -                   |

> 更多用法可以查看 [Descriptions](https://ant.design/components/descriptions-cn/) 。



# useModal

## 弹窗表单

在 Modal 里使用的表单，一般调用 useModal 来使用它，常用在表单操作项。

显示Modal效果

![image-20241205055504804](/Users/majirong/Library/Application Support/typora-user-images/image-20241205055504804.png)

填充值效果

![image-20241205055547786](/Users/majirong/Library/Application Support/typora-user-images/image-20241205055547786.png)

```tsx
import React, { useMemo } from 'react';
import { Button, Space, Form, Radio, Input } from 'antd';
import { useModal, PortalProvider, ArrSelect } from 'parsec-admin';

const Demo = () => {
  const [form] = Form.useForm();
  const switchModalVisible = useModal(
    {
      title: '新增用户',
      form,
      items: [
        {
          label: '姓名',
          name: 'name',
          required: true,
        },
        ({ name = '' }) => ({
          label: `${name}的年龄`,
          name: 'age',
          required: true,
        }),
        {
          label: `自定义xxx`,
          name: 'customize',
          render: (
            <Radio.Group
              onChange={e => {
                if (e.target.value) {
                  form.resetFields(['xxx']);
                } else {
                  form.setFieldsValue({ xxx: 123 });
                }
              }}
            >
              <Radio value={true}>是</Radio>
              <Radio value={false}>否</Radio>
            </Radio.Group>
          ),
        },
        {
          label: `xxx`,
          name: 'xxx',
          render: (_, {customize}) => (
            <Input disabled={!customize}/>
          ),
        },
        {
          label: '性别',
          name: 'sex',
          labelName: 'sexName',
          render: <ArrSelect options={[{value: 1, label: '男'}, {value: 2, label: '女'}]}/>
        }
      ],
      onSubmit: (values) => {
        alert(JSON.stringify(values));
        return new Promise(resolve => setTimeout(resolve, 1000))
      },
    },
    // 如果modal里用了state，请在下面添加依赖
    [],
  );
  return (
    <Space>
      <Button type={'primary'} onClick={() => switchModalVisible()}>
        显示 Modal
      </Button>
      <Button
        type={'primary'}
        onClick={() => switchModalVisible({ name: '姓名', age: '18' })}
      >
        填充值
      </Button>
    </Space>
  );
};

export default () => (
  <PortalProvider>
    <Demo />
  </PortalProvider>
);
```

### API

| 属性        | 说明                                                         | 默认值              |
| ----------- | ------------------------------------------------------------ | ------------------- |
| form        | 自定义 form 实例。                                           | `form.useForm()[0]` |
| onSubmit    | 提交事件，当 form 检验完后会触发这个事件，需要返回一个 Promise 方法。 | -                   |
| items       | 表单项。                                                     | -                   |
| myFormProps | form [props](/components/form#api) 。                        | -                   |

> 更多用法可以查看 [Modal](https://ant.design/components/modal-cn/#API) 。



# InlineFormItemWrap

## 行内表单项

当 Form.Item 里需要包含好几个表单项时可以用这个包裹。

效果图

![image-20241205055845030](/Users/majirong/Library/Application Support/typora-user-images/image-20241205055845030.png)

```tsx
import React from 'react';
import { InputNumber } from 'antd';
import { InlineFormItemWrap, Form } from 'parsec-admin';

export default () => (
  <Form
    onSubmit={values => {
      console.log(values);
      return Promise.resolve();
    }}
    items={[
      {
        label: '范围',
        required: true,
        render: (
          <InlineFormItemWrap>
            <Form.Item
              name={'min'}
              rules={[{ required: true, message: '请输入最小值' }]}
            >
              <InputNumber placeholder={'最小值'} />
            </Form.Item>
            <span>至</span>
            <Form.Item
              name={'max'}
              rules={[{ required: true, message: '请输入最大值' }]}
            >
              <InputNumber placeholder={'最大值'} />
            </Form.Item>
          </InlineFormItemWrap>
        ),
      },
      {
        label: '百分比',
        required: true,
        render: (
          <InlineFormItemWrap>
            <Form.Item
              name={'percent'}
              rules={[{ required: true, message: '请输入百分比' }]}
            >
              <InputNumber placeholder={'请输入'} />
            </Form.Item>
            <span>%</span>
          </InlineFormItemWrap>
        ),
      },
    ]}
  />
);
```

### API

| 属性             | 说明                 | 默认值  |
| ---------------- | -------------------- | ------- |
| hideRequiredMark | 隐藏必填项的 \* 号。 | `false` |



# InputMoney

## 金额输入

用于输入以分为单位的输入框，以分为单位传入，会以元显示，提交则又会转换为以分单位。

效果图

![image-20241205060044613](/Users/majirong/Library/Application Support/typora-user-images/image-20241205060044613.png)

```tsx
import React from 'react';
import { InputMoney } from 'parsec-admin';
import { useForceUpdate, useInit } from 'parsec-hooks';
import { Form } from 'antd';

const FormItem = Form.Item;

export default () => {
  const { forceUpdate } = useForceUpdate();
  // 第一次进来更新一下
  useInit(forceUpdate);
  const [form] = Form.useForm();
  return (
    <Form
      form={form}
      // 每次输入强制更新，让下面的 moneyValue 能同步更新
      onValuesChange={forceUpdate}
      initialValues={{ money: 1000 }}
    >
      <FormItem label={'金额'} name={'money'}>
        <InputMoney unit={'元'} />
      </FormItem>
      <br />
      moneyValue: {form.getFieldValue('money')}
    </Form>
  );
};
```

### API

| 属性 | 说明                   | 默认值 |
| ---- | ---------------------- | ------ |
| unit | input 后面显示的单位。 | -      |

> 更多使用方法查看 [InputNumber](https://ant.design/components/input-number-cn/#API) 。





# LinkButton

## 链接按钮

跟 a 标签一样样式的按钮。

效果图

![image-20241205060646559](/Users/majirong/Library/Application Support/typora-user-images/image-20241205060646559.png)

```tsx
import React from 'react';
import { LinkButton } from 'parsec-admin';
import { message } from 'antd';

export default () => (
  <LinkButton onClick={() => message.success('我是按钮')}>我是按钮</LinkButton>
);
```

### 同时使用多个

通常跟 ActionsWrap 配合在 Table 里使用。

效果图

![image-20241205060701598](/Users/majirong/Library/Application Support/typora-user-images/image-20241205060701598.png)

```tsx
import React from 'react';
import { LinkButton, ActionsWrap } from 'parsec-admin';

export default () => (
  <ActionsWrap>
    <LinkButton>编辑</LinkButton>
    <LinkButton>详情</LinkButton>
    <LinkButton>删除</LinkButton>
  </ActionsWrap>
);
```



# PageHeader

## 页头

默认不需要设置 `breadcrumb` 和 `title` 也会根据 App routes 配置自动显示。

效果图

![image-20241205061338307](/Users/majirong/Library/Application Support/typora-user-images/image-20241205061338307.png)

```tsx
/**
 * background: '#f6f7f9'
 */
import React from 'react';
import { PageHeader } from 'parsec-admin';
import { Button, Descriptions } from 'antd';

export default () => (
  <PageHeader
    ghost={false}
    onBack={() => window.history.back()}
    title="Title"
    subTitle="This is a subtitle"
    extra={[
      <Button key="3">Operation</Button>,
      <Button key="2">Operation</Button>,
      <Button key="1" type="primary">
        Primary
      </Button>,
    ]}
  >
    <Descriptions size="small" column={3}>
      <Descriptions.Item label="Created">Lili Qu</Descriptions.Item>
      <Descriptions.Item label="Association">
        <a>421421</a>
      </Descriptions.Item>
      <Descriptions.Item label="Creation Time">2017-01-10</Descriptions.Item>
      <Descriptions.Item label="Effective Time">2017-10-10</Descriptions.Item>
      <Descriptions.Item label="Remarks">
        Gonghu Road, Xihu District, Hangzhou, Zhejiang, China
      </Descriptions.Item>
    </Descriptions>
  </PageHeader>
);
```

### 粘性定位

设置 `sticky` 后，可实现粘性定位。

```tsx
/**
 * background: '#f6f7f9'
 */
import React from 'react';
import { PageHeader, BlankSection } from 'parsec-admin';
import { Button, Descriptions, Typography, Divider } from 'antd';
import styled from 'styled-components';

const { Title, Paragraph, Text } = Typography;

const Page = styled.div`
  height: 500px;
  overflow: auto;
`;

export default () => (
  <Page>
    <PageHeader
      sticky
      ghost={false}
      onBack={() => window.history.back()}
      title="Title"
      subTitle="This is a subtitle"
      extra={[
        <Button key="3">Operation</Button>,
        <Button key="2">Operation</Button>,
        <Button key="1" type="primary">
          Primary
        </Button>,
      ]}
    >
      <Descriptions size="small" column={3}>
        <Descriptions.Item label="Created">Lili Qu</Descriptions.Item>
        <Descriptions.Item label="Association">
          <a>421421</a>
        </Descriptions.Item>
        <Descriptions.Item label="Creation Time">2017-01-10</Descriptions.Item>
        <Descriptions.Item label="Effective Time">2017-10-10</Descriptions.Item>
        <Descriptions.Item label="Remarks">
          Gonghu Road, Xihu District, Hangzhou, Zhejiang, China
        </Descriptions.Item>
      </Descriptions>
    </PageHeader>
    <BlankSection>
      <Typography>
        <Title>Introduction</Title>
        <Paragraph>
          In the process of internal desktop applications development, many
          different design specs and implementations would be involved, which
          might cause designers and developers difficulties and duplication and
          reduce the efficiency of development.
        </Paragraph>
        <Paragraph>
          After massive project practice and summaries, Ant Design, a design
          language for background applications, is refined by Ant UED Team,
          which aims to
          <Text strong>
            uniform the user interface specs for internal background projects,
            lower the unnecessary cost of design differences and implementation
            and liberate the resources of design and front-end development
          </Text>.
        </Paragraph>
        <Title level={2}>Guidelines and Resources</Title>
        <Paragraph>
          We supply a series of design principles, practical patterns and high
          quality design resources (<Text code>Sketch</Text> and{' '}
          <Text code>Axure</Text>), to help people create their product
          prototypes beautifully and efficiently.
        </Paragraph>

        <Paragraph>
          <ul>
            <li>
              <a>Principles</a>
            </li>
            <li>
              <a>Patterns</a>
            </li>
            <li>
              <a>Resource Download</a>
            </li>
          </ul>
        </Paragraph>

        <Divider />

        <Title>介绍</Title>
        <Paragraph>
          蚂蚁的企业级产品是一个庞大且复杂的体系。这类产品不仅量级巨大且功能复杂，而且变动和并发频繁，常常需要设计与开发能够快速的做出响应。同时这类产品中有存在很多类似的页面以及组件，可以通过抽象得到一些稳定且高复用性的内容。
        </Paragraph>
        <Paragraph>
          随着商业化的趋势，越来越多的企业级产品对更好的用户体验有了进一步的要求。带着这样的一个终极目标，我们（蚂蚁金服体验技术部）经过大量的项目实践和总结，逐步打磨出一个服务于企业级产品的设计体系
          Ant Design。基于<Text mark>『确定』和『自然』</Text>
          的设计价值观，通过模块化的解决方案，降低冗余的生产成本，让设计者专注于
          <Text strong>更好的用户体验</Text>。
        </Paragraph>
        <Title level={2}>设计资源</Title>
        <Paragraph>
          我们提供完善的设计原则、最佳实践和设计资源文件（
          <Text code>Sketch</Text> 和<Text code>Axure</Text>
          ），来帮助业务快速设计出高质量的产品原型。
        </Paragraph>

        <Paragraph>
          <ul>
            <li>
              <a>设计原则</a>
            </li>
            <li>
              <a>设计模式</a>
            </li>
            <li>
              <a>设计资源</a>
            </li>
          </ul>
        </Paragraph>
      </Typography>
    </BlankSection>
  </Page>
);
```

### API

| 属性   | 说明         | 默认值  |
| ------ | ------------ | ------- |
| sticky | 是否粘性定位 | `false` |

> 更多使用方法查看 [PageHeader](https://ant.design/components/page-header-cn/#API) 。





# PreviewImg

## 预览图片

点击后可以预览的图片的组件。

```tsx
import React from 'react';
import { PreviewImg } from 'parsec-admin';

export default () => (
  <PreviewImg
    src={'https://gw.alipayobjects.com/zos/rmsportal/rlpTLlbMzTNYuZGGCVYM.png'}
  />
);
```

### 其他组件控制

`children` 传入什么，界面就会显示什么，点击后就会预览图片。

```tsx
import React from 'react';
import { PreviewImg } from 'parsec-admin';
import { Button } from 'antd';

export default () => (
  <div>
    <PreviewImg
      src={'https://gw.alipayobjects.com/zos/rmsportal/rlpTLlbMzTNYuZGGCVYM.png'}
    >
      <Button type={'primary'}>显示图片</Button>
    </PreviewImg>
    <PreviewImg
      src={['https://gw.alipayobjects.com/zos/rmsportal/rlpTLlbMzTNYuZGGCVYM.png','https://gw.alipayobjects.com/zos/rmsportal/rlpTLlbMzTNYuZGGCVYM.png']}
    >
      <Button type={'primary'}>显示多张图片</Button>
    </PreviewImg>
  </div>
);
```



# QQMap

## 地图定位

可以直接在 FormItem 里使用的地图定位选择组件。

效果图

![image-20241205061814080](/Users/majirong/Library/Application Support/typora-user-images/image-20241205061814080.png)

```tsx
import React from 'react';
import { Form, QQMap } from 'parsec-admin';

export default () => (
  <Form
    items={[
      {
        name: 'gps',
        required: true,
        label: '医院地址',
        formItemProps: {
          initialValue: {
            address: '重庆市渝北区红锦大道89号',
            lat: 29.595399,
            lng: 106.521407,
          },
        },
        render: <QQMap />,
      },
    ]}
    layout={{
      labelCol: {
        span: 4,
      },
    }}
  />
);
```

### API

| 属性     | 说明                                                         | 默认值 |
| -------- | ------------------------------------------------------------ | ------ |
| key      | 可以设置自己的腾讯地图 key ，具体部署的项目需要加域名白名单  | -      |
| onChange | (value) => void                                              | -      |
| value    | {address?:string; lat?:number 或 string; lng?: number 或 string;} | -      |



# StatisticalStr

## 统计字符串

显示统计值的大概数值。

效果图

![image-20241205062103652](/Users/majirong/Library/Application Support/typora-user-images/image-20241205062103652.png)

```tsx
import React from 'react';
import { StatisticalStr } from 'parsec-admin';
import { Space } from 'antd';

export default () => (
  <Space>
    <StatisticalStr value={1000} />
    <StatisticalStr value={12342} unit={'人'} />
    <StatisticalStr value={534432} unit={'元'} />
    <StatisticalStr value={6545324} unit={'字节'} />
  </Space>
);
```

### API

| 属性  | 说明                 | 默认值 |
| ----- | -------------------- | ------ |
| unit  | 数值后面显示的单位。 | -      |
| value | 数值。               | -      |



# Upload，UploadBtn，UploadImg

## 上传

可以直接在 FormItem 里使用的上传组件。

效果图

![image-20241205062324486](/Users/majirong/Library/Application Support/typora-user-images/image-20241205062324486.png)

```tsx
import React from 'react';
import { Form, Upload, UploadBtn, UploadImg } from 'parsec-admin';
import DocuApp from '../../AloneRouteDocuApp'

export default () => (
  <DocuApp>
    <Form
      items={[
        {
          name: 'file',
          required: true,
          label: '上传组件',
          render: <Upload><div style={{width: 100, height: 100, background: '#eee'}}>点击、拖拽上传</div></Upload>,
        },
        {
          name: 'btn',
          required: true,
          label: '上传按钮',
          render: <UploadBtn/>,
        },
        {
          name: 'img',
          required: true,
          label: '上传图片',
          render: <UploadImg/>,
        },
      ]}
    />
  </DocuApp>
);
```

### API

| 属性             | 说明                                         | 默认值 |
| ---------------- | -------------------------------------------- | ------ |
| length           | 允许上传的文件数量。                         | 1      |
| renderFileName   | 渲染文件名。                                 | -      |
| maxSize          | 上传文件最大大小。                           | -      |
| onMaxError       | 超出限制大小事件。                           | -      |
| arrValue         | 当length===1时生效，是否返回数组value。      | `true` |
| onFileListChange | 当fileList改变时会执行。                     | -      |
| fileValue        | 返回file类型的值，不再通过上传方法进行上传。 | -      |



---
# WaterMark

## 水印组件

给页面的某个区域加上水印。

## 何时使用

页面需要添加水印标识版权时使用。
更多使用访问这里：[https://procomponents.ant.design/components/water-mark](https://procomponents.ant.design/components/water-mark)

效果图

![image-20241205062518288](/Users/majirong/Library/Application Support/typora-user-images/image-20241205062518288.png)

## 代码演示

### 文字水印

通过 `content` 指定文字水印内容。

```tsx
/** Title: 文字水印 */
import React from 'react';
import { WaterMark } from 'parsec-admin';

export default () => (
  <WaterMark content="秒差距科技">
    <div style={{ height: 300 }} />
  </WaterMark>
);
```

### 图片水印

通过 `image` 指定图片地址。为保证图片高清且不被拉伸，请传入水印图片的宽高 width 和 height, 并上传至少两倍的宽高的 logo 图片地址。

```tsx
/** Title: 图片水印 */
import React from 'react';
import { WaterMark } from 'parsec-admin';

export default () => {
  return (
    <WaterMark
      height={36}
      width={115}
      image="https://gw.alipayobjects.com/zos/bmw-prod/59a18171-ae17-4fc5-93a0-2645f64a3aca.svg"
    >
      <div style={{ height: 500 }}>
        <p>
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quisquam
          aliquid perferendis, adipisci dolorum officia odio natus facere cumque
          iusto libero repellendus praesentium ipsa cupiditate iure autem eos
          repudiandae delectus totam?
        </p>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Illo
          praesentium, aperiam numquam voluptatibus asperiores odio? Doloribus
          saepe, eligendi facere inventore culpa, exercitationem explicabo earum
          laborum deleniti reiciendis deserunt accusantium ullam.
        </p>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Officia
          voluptas numquam impedit architecto facilis aliquam at assumenda,
          nostrum explicabo accusantium ipsam error provident voluptate
          molestias magnam quisquam excepturi illum sit!
        </p>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam,
          accusantium quo corporis fugit possimus quaerat ad consequatur veniam
          voluptatum ut cumque illo beatae. Magni assumenda eligendi itaque eum
          voluptate non!
        </p>
      </div>
    </WaterMark>
  );
};
```

## API

### 基础参数

| 参数      | 说明                                                 | 类型                 | 默认值            | 版本  |
| --------- | ---------------------------------------------------- | -------------------- | ----------------- | ----- |
| width     | 水印的宽度                                           | number               | 120               | 2.2.0 |
| height    | 水印的高度                                           | number               | 64                | 2.2.0 |
| rotate    | 水印绘制时，旋转的角度，单位 °                       | number               | -22               | 2.2.0 |
| image     | 图片源，建议导出 2 倍或 3 倍图，优先使用图片渲染水印 | `string`             | -                 | 2.2.0 |
| zIndex    | 追加的水印元素的 z-index                             | number               | 9                 | 2.2.0 |
| content   | 水印文字内容                                         | `string`             | -                 | 2.2.0 |
| fontColor | 水印文字颜色                                         | `string`             | `rgba(0,0,0,.15)` | 2.2.0 |
| fontSize  | 文字大小                                             | `string` \| `number` | 16                | 2.2.0 |

### 高级参数

| 参数          | 说明                                                         | 类型                | 默认值                 | 版本  |
| ------------- | ------------------------------------------------------------ | ------------------- | ---------------------- | ----- |
| markStyle     | 水印层的样式                                                 | React.CSSProperties | -                      | 2.3.0 |
| markClassName | 水印层的类名                                                 | string              | -                      | 2.3.0 |
| gapX          | 水印之间的水平间距                                           | number              | 212                    | 2.4.0 |
| gapY          | 水印之间的垂直间距                                           | number              | 222                    | 2.4.0 |
| offsetLeft    | 水印在 canvas 画布上绘制的水平偏移量, 正常情况下，水印绘制在中间位置, 即 `offsetTop = gapX / 2` | number              | `offsetTop = gapX / 2` | 2.4.0 |
| offsetTop     | 水印在 canvas 画布上绘制的垂直偏移量，正常情况下，水印绘制在中间位置, 即 `offsetTop = gapY / 2` | number              | `offsetTop = gapY / 2` | 2.4.0 |

### 水印 API 可视化

```jsx | inline
import react from 'react';

export default () => (
  <div>
    <img
      src="https://gw.alipayobjects.com/zos/alicdn/joeXYy8j3/jieping2021-01-11%252520xiawu4.47.15.png"
      width="100%"
    />
  </div>
);
```
