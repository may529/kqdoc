---
nav:
  title: 组件
  path: /components
group:
  title: 通用
  path: /general
---

## Modal 弹框

弹窗

```tsx
import React, { useState } from 'react';
import {
  Space,
  PartTitle,
  Button,
  Modal,
  showToast,
  ReInput,
  Form,
  FormItem,
  rpxToPx,
} from '@kqinfo/ui';

export default () => {
  const [readOnly, setReadOnly] = useState(false);
  const [form] = Form.useForm();
  return (
    <Space vertical size={'10px'} alignItems={'stretch'}>
      <Modal />
      <PartTitle>一般用法</PartTitle>
      <Button
        type={'primary'}
        onTap={() =>
          Modal.show({
            title: '发送报告至邮箱',
            onOk: () =>
              new Promise((resolve, reject) => {
                setTimeout(() => {
                  form.submit();
                  form
                    .validateFields()
                    .then(values => {
                      alert(JSON.stringify(values));
                      return resolve('ok');
                    })
                    .catch(reject);
                }, 3000);
              }),
            content: (
              <Form form={form} style={{ width: '100%' }}>
                <FormItem
                  noStyle
                  name={'email'}
                  rules={[
                    { type: 'email', message: '请输入正确的邮箱' },
                    { required: true, message: '请输入邮箱' },
                  ]}
                >
                  <ReInput
                    style={{
                      background: '#F1F1F1',
                      borderRadius: rpxToPx(20),
                      height: rpxToPx(90),
                      width: '100%',
                      boxSizing: 'border-box',
                      padding: `0 ${rpxToPx(31)}px`,
                    }}
                    placeholder={'请输入邮箱号码'}
                  />
                </FormItem>
              </Form>
            ),
          })
            .then(() => {
              showToast({ title: '确定' });
            })
            .catch(() => {
              showToast({ title: '取消' });
            })
        }
      >
        显示
      </Button>
      <Button
        type={'primary'}
        onTap={() =>
          Modal.show({
            title: '手动隐藏',
            maskClosable: false,
            content: <Button onTap={() => Modal.hide()}>隐藏</Button>,
            footer: null,
          })
        }
      >
        禁止点击背景，手动隐藏
      </Button>
      <PartTitle>自定义确认文字与颜色</PartTitle>
      <Button
        type={'primary'}
        onTap={() =>
          Modal.show({
            title: '发送',
            content: '确认发送',
            okText: '发送',
            okTextColor: '#165DFF',
          })
        }
      >
        自定义确认文字与颜色
      </Button>
      <PartTitle>无取消按钮</PartTitle>
      <Button
        onTap={() =>
          Modal.show({
            title: '提示',
            content: '仅显示确定',
            showCancel: false,
          })
        }
      >
        隐藏取消按钮
      </Button>
      <PartTitle>自定义宽度与类名</PartTitle>
      <style>{`
        .myWrap { border: 1px solid #eee; border-radius: 12px; }
        .myTitle { font-weight: 600; }
        .myBody { background: #fafafa; }
        .myContent { padding: 16px; }
        .myFooter { }
        .myBtn { }
        .myOk { }
      `}</style>
      <Button
        onTap={() =>
          Modal.show({
            title: '自定义样式',
            content: '设置宽度为 600rpx，并注入自定义类名',
            width: 600,
            className: 'myWrap',
            titleCls: 'myTitle',
            bodyCls: 'myBody',
            contentCls: 'myContent',
            footerCls: 'myFooter',
            btnCls: 'myBtn',
            okCls: 'myOk',
          })
        }
      >
        自定义宽度与类名
      </Button>
    </Space>
  );
};
```

<API exports='["default", "Options"]'></API>
