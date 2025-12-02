# OpenForAll 微信开发 SDK - Node.js版

<div align="center">

![OpenForAll Logo](https://img.shields.io/badge/OpenForAll-微信开发SDK-blue)
[![Node Version](https://img.shields.io/badge/Node-%3E%3D12.0-339933.svg)](https://nodejs.org/)
[![NPM version](https://img.shields.io/npm/v/openforall-sdk.svg)](https://www.npmjs.com/package/openforall-sdk)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Downloads](https://img.shields.io/npm/dm/openforall-sdk.svg)](https://www.npmjs.com/package/openforall-sdk)

**🚀 企业级微信API开发工具包 | 5分钟快速接入 | TypeScript支持**

[快速开始](#快速开始) • [在线演示](https://openforall.liebianjun.com/sdk/nodejs/demo/) • [完整文档](https://openforall.liebianjun.com/docs) • [API参考](#api文档)

</div>

---

## ✨ 核心特性

### 🎯 功能全面
- ✅ **微信支付** - 扫码支付、公众号支付、APP支付、H5支付
- ✅ **微信授权** - OAuth2.0授权登录、用户信息获取
- ✅ **微信红包** - 现金红包、裂变红包、企业付款
- ✅ **用户管理** - 注册、登录、资料管理、权限控制
- ✅ **支付宝支付** - PC支付、手机支付、扫码支付
- ✅ **短信验证** - 阿里云、腾讯云短信接口
- ✅ **邮件服务** - 验证码、通知邮件
- ✅ **文件上传** - 图片、文档、视频上传

### 💚 现代化设计
- 🎨 **TypeScript** - 完整的类型定义
- 🔄 **Promise/Async** - 支持Promise和async/await
- 📦 **ES6+** - 使用现代JavaScript特性
- 🧪 **测试覆盖** - 完善的单元测试

### 🔒 安全可靠
- 🛡️ **金融级安全** - 签名验证、加密传输、防重放攻击
- 🔐 **权限控制** - 基于角色的访问控制(RBAC)
- 📝 **完整日志** - 操作日志、错误日志、审计日志
- ⚡ **高性能** - 连接池、缓存优化、异步处理

---

## 📋 目录

- [系统要求](#系统要求)
- [快速开始](#快速开始)
- [安装方式](#安装方式)
- [配置说明](#配置说明)
- [使用示例](#使用示例)
- [TypeScript支持](#typescript支持)
- [API文档](#api文档)
- [常见问题](#常见问题)
- [贡献指南](#贡献指南)
- [技术支持](#技术支持)

---

## 🔧 系统要求

- **Node.js** >= 12.0
- **npm** >= 6.0 或 **yarn** >= 1.22

---

## 🚀 快速开始

### 安装

```bash
npm install openforall-sdk
# 或
yarn add openforall-sdk
```

### 基础使用

```javascript
const { OpenForAllClient } = require('openforall-sdk');

// 1. 配置初始化
const config = {
  apiKey: 'your_api_key',
  apiSecret: 'your_api_secret',
  apiUrl: 'https://openforall.liebianjun.com'
};

// 2. 创建客户端
const client = new OpenForAllClient(config);

// 3. 用户登录
async function login() {
  try {
    const result = await client.userLogin('username', 'password');
    console.log('登录成功！Token:', result.data.token);
  } catch (error) {
    console.error('登录失败:', error.message);
  }
}

login();
```

### ES6模块

```javascript
import { OpenForAllClient } from 'openforall-sdk';

const client = new OpenForAllClient(config);

// 使用 async/await
const result = await client.userLogin('username', 'password');
```

---

## 📦 安装方式

### NPM安装（推荐）

```bash
npm install openforall-sdk --save
```

### Yarn安装

```bash
yarn add openforall-sdk
```

### 从源码安装

```bash
git clone https://github.com/openforall/wechat-sdk-nodejs.git
cd wechat-sdk-nodejs
npm install
npm run build
```

---

## ⚙️ 配置说明

### 基础配置

```javascript
const config = {
  // API密钥（必填）
  apiKey: 'your_api_key_here',
  
  // API密钥（必填）
  apiSecret: 'your_api_secret_here',
  
  // API地址（必填）
  apiUrl: 'https://your-domain.com',
  
  // 调试模式（可选）
  debug: false,
  
  // 超时时间（可选，毫秒）
  timeout: 30000,
  
  // 日志路径（可选）
  logPath: '/path/to/logs',
};

const client = new OpenForAllClient(config);
```

### 环境变量配置（推荐）

```javascript
// .env 文件
OPENFORALL_API_KEY=your_api_key
OPENFORALL_API_SECRET=your_api_secret
OPENFORALL_API_URL=https://openforall.liebianjun.com

// 代码中使用
require('dotenv').config();

const config = {
  apiKey: process.env.OPENFORALL_API_KEY,
  apiSecret: process.env.OPENFORALL_API_SECRET,
  apiUrl: process.env.OPENFORALL_API_URL,
};
```

---

## 💡 使用示例

### 用户注册与登录

```javascript
const { OpenForAllClient } = require('openforall-sdk');

const client = new OpenForAllClient(config);

async function userDemo() {
  try {
    // 1. 发送短信验证码
    await client.sendSms('13800138000', 'register');
    
    // 2. 用户注册
    const registerResult = await client.userRegister({
      username: 'testuser',
      password: 'password123',
      email: 'test@example.com',
      mobile: '13800138000',
      code: '123456'
    });
    
    // 3. 用户登录
    const loginResult = await client.userLogin('testuser', 'password123');
    
    const token = loginResult.data.token;
    const userInfo = loginResult.data.userinfo;
    
    console.log('登录成功！用户ID:', userInfo.id);
    
    // 4. 手机验证码登录
    const mobileLoginResult = await client.userMobileLogin('13800138000', '123456');
    
  } catch (error) {
    console.error('错误:', error.message);
  }
}

userDemo();
```

### 微信支付

```javascript
async function wechatPayDemo() {
  try {
    // 1. 创建支付订单
    const orderResult = await client.createPayment({
      type: 'package',
      paymentMethod: 'wechat',
      packageId: 1,
      orderNo: `ORD${Date.now()}`,
      amount: 99.00
    });
    
    const billId = orderResult.data.bill_id;
    
    // 2. 发起微信扫码支付
    const payResult = await client.wechatPay(billId, 'NATIVE');
    
    const qrcodeUrl = payResult.data.code_url;
    console.log('请扫码支付:', qrcodeUrl);
    
    // 3. 轮询查询支付状态
    const checkPayment = setInterval(async () => {
      const statusResult = await client.queryPayment(orderResult.data.order_no);
      
      if (statusResult.data.status === 'paid') {
        console.log('支付成功！');
        clearInterval(checkPayment);
      }
    }, 3000);
    
  } catch (error) {
    console.error('支付错误:', error.message);
  }
}

wechatPayDemo();
```

### 支付宝支付

```javascript
async function alipayDemo() {
  try {
    // 1. 创建支付订单
    const orderResult = await client.createPayment({
      type: 'package',
      paymentMethod: 'alipay',
      packageId: 1,
      orderNo: `ORD${Date.now()}`,
      amount: 99.00
    });
    
    // 2. 发起支付宝支付
    const payResult = await client.alipay(orderResult.data.bill_id);
    
    // 3. 跳转到支付宝支付页面
    const payUrl = payResult.data.pay_url;
    console.log('支付链接:', payUrl);
    
  } catch (error) {
    console.error('支付错误:', error.message);
  }
}

alipayDemo();
```

### 用户信息管理

```javascript
async function userInfoDemo() {
  try {
    // 获取用户信息
    const userResult = await client.getUserInfo();
    const userInfo = userResult.data;
    
    console.log('用户名:', userInfo.username);
    console.log('余额:', userInfo.money);
    
    // 修改用户资料
    await client.updateProfile({
      nickname: '新昵称',
      bio: '个人简介',
      avatar: 'https://example.com/avatar.jpg'
    });
    
    // 修改邮箱
    await client.changeEmail('newemail@example.com', '123456');
    
    // 修改手机号
    await client.changeMobile('13900139000', '123456');
    
    // 重置密码
    await client.resetPassword('13800138000', '123456', 'newpassword');
    
  } catch (error) {
    console.error('错误:', error.message);
  }
}

userInfoDemo();
```

### 文件上传

```javascript
const fs = require('fs');

async function uploadDemo() {
  try {
    // 方式1: 使用文件路径
    const result1 = await client.uploadFile('/path/to/image.jpg');
    console.log('上传成功:', result1.data.url);
    
    // 方式2: 使用Buffer
    const fileBuffer = fs.readFileSync('/path/to/image.jpg');
    const result2 = await client.uploadFile(fileBuffer, 'image.jpg');
    
    // 方式3: 使用Stream
    const fileStream = fs.createReadStream('/path/to/image.jpg');
    const result3 = await client.uploadFile(fileStream, 'image.jpg');
    
  } catch (error) {
    console.error('上传错误:', error.message);
  }
}

uploadDemo();
```

### 短信和邮件验证

```javascript
async function verificationDemo() {
  try {
    // 发送短信验证码
    await client.sendSms('13800138000', 'register');
    
    // 验证短信验证码
    const smsResult = await client.verifySms('13800138000', '123456', 'register');
    
    // 发送邮件验证码
    await client.sendEmail('test@example.com', 'register');
    
    // 验证邮件验证码
    const emailResult = await client.verifyEmail('test@example.com', '123456', 'register');
    
  } catch (error) {
    console.error('错误:', error.message);
  }
}

verificationDemo();
```

---

## 📘 TypeScript支持

SDK提供完整的TypeScript类型定义：

```typescript
import { OpenForAllClient, UserLoginResult, PaymentResult } from 'openforall-sdk';

const config: ClientConfig = {
  apiKey: 'your_api_key',
  apiSecret: 'your_api_secret',
  apiUrl: 'https://openforall.liebianjun.com'
};

const client = new OpenForAllClient(config);

// 类型安全的API调用
async function login(): Promise<void> {
  try {
    const result: UserLoginResult = await client.userLogin('username', 'password');
    const token: string = result.data.token;
    console.log('Token:', token);
  } catch (error) {
    console.error('Error:', error);
  }
}

// 支付接口
async function createPayment(): Promise<void> {
  const paymentData: PaymentRequest = {
    type: 'package',
    paymentMethod: 'wechat',
    packageId: 1,
    orderNo: `ORD${Date.now()}`,
    amount: 99.00
  };
  
  const result: PaymentResult = await client.createPayment(paymentData);
}
```

### 类型定义

```typescript
// 配置类型
interface ClientConfig {
  apiKey: string;
  apiSecret: string;
  apiUrl: string;
  debug?: boolean;
  timeout?: number;
  logPath?: string;
}

// 用户登录结果
interface UserLoginResult {
  code: number;
  msg: string;
  data: {
    token: string;
    userinfo: UserInfo;
  };
}

// 支付请求
interface PaymentRequest {
  type: 'package' | 'bill';
  paymentMethod: 'wechat' | 'alipay' | 'balance';
  packageId?: number;
  orderNo: string;
  amount: number;
  couponId?: number;
  discountAmount?: number;
}
```

---

## 📚 API文档

### 用户接口

| 方法 | 说明 | 参数 |
|------|------|------|
| `userRegister()` | 用户注册 | username, password, email, mobile, code |
| `userLogin()` | 账号登录 | account, password |
| `userMobileLogin()` | 手机验证码登录 | mobile, captcha |
| `getUserInfo()` | 获取用户信息 | - |
| `updateProfile()` | 修改用户资料 | data: object |
| `changeEmail()` | 修改邮箱 | email, code |
| `changeMobile()` | 修改手机号 | mobile, code |
| `resetPassword()` | 重置密码 | mobile, code, newpassword |
| `userLogout()` | 退出登录 | - |

### 支付接口

| 方法 | 说明 | 参数 |
|------|------|------|
| `createPayment()` | 创建支付订单 | data: object |
| `wechatPay()` | 微信支付 | billId, tradeType, openid |
| `alipay()` | 支付宝支付 | billId |
| `balancePay()` | 余额支付 | billId, requestId |
| `balancePayPackage()` | 余额支付套餐 | data: object |
| `queryPayment()` | 查询支付状态 | orderNo |
| `cancelPayment()` | 取消支付 | orderNo |

### 短信和邮件接口

| 方法 | 说明 | 参数 |
|------|------|------|
| `sendSms()` | 发送短信验证码 | mobile, event |
| `verifySms()` | 验证短信验证码 | mobile, code, event |
| `sendEmail()` | 发送邮件验证码 | email, event |
| `verifyEmail()` | 验证邮件验证码 | email, code, event |

### 公共接口

| 方法 | 说明 | 参数 |
|------|------|------|
| `init()` | 初始化配置 | version, lng, lat |
| `uploadFile()` | 上传文件 | file, filename |
| `getCaptcha()` | 获取验证码 | id |

---

## 🔍 错误处理

### Promise方式

```javascript
client.userLogin('username', 'password')
  .then(result => {
    console.log('登录成功:', result.data);
  })
  .catch(error => {
    console.error('登录失败:', error.message);
  });
```

### Async/Await方式

```javascript
async function login() {
  try {
    const result = await client.userLogin('username', 'password');
    console.log('登录成功:', result.data);
  } catch (error) {
    console.error('登录失败:', error.message);
    
    // 错误类型判断
    if (error.code === 401) {
      console.error('认证失败');
    } else if (error.code === 422) {
      console.error('参数验证失败');
    }
  }
}
```

### 自定义错误处理

```javascript
const client = new OpenForAllClient({
  ...config,
  onError: (error) => {
    // 自定义错误处理
    console.error('SDK Error:', error);
    
    // 发送到错误监控服务
    // errorMonitor.report(error);
  }
});
```

---

## ❓ 常见问题

### 1. 如何在Express中使用？

```javascript
const express = require('express');
const { OpenForAllClient } = require('openforall-sdk');

const app = express();
const client = new OpenForAllClient(config);

app.post('/api/login', async (req, res) => {
  try {
    const { username, password } = req.body;
    const result = await client.userLogin(username, password);
    res.json(result);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3000);
```

### 2. 如何在Koa中使用？

```javascript
const Koa = require('koa');
const Router = require('koa-router');
const { OpenForAllClient } = require('openforall-sdk');

const app = new Koa();
const router = new Router();
const client = new OpenForAllClient(config);

router.post('/api/login', async (ctx) => {
  try {
    const { username, password } = ctx.request.body;
    const result = await client.userLogin(username, password);
    ctx.body = result;
  } catch (error) {
    ctx.status = 500;
    ctx.body = { error: error.message };
  }
});

app.use(router.routes());
app.listen(3000);
```

### 3. 如何在Nest.js中使用？

```typescript
import { Injectable } from '@nestjs/common';
import { OpenForAllClient } from 'openforall-sdk';

@Injectable()
export class OpenForAllService {
  private client: OpenForAllClient;
  
  constructor() {
    this.client = new OpenForAllClient({
      apiKey: process.env.OPENFORALL_API_KEY,
      apiSecret: process.env.OPENFORALL_API_SECRET,
      apiUrl: process.env.OPENFORALL_API_URL,
    });
  }
  
  async login(username: string, password: string) {
    return await this.client.userLogin(username, password);
  }
}
```

### 4. 如何处理并发请求？

```javascript
async function concurrentRequests() {
  // 使用 Promise.all 并发执行
  const [user, payment1, payment2] = await Promise.all([
    client.getUserInfo(),
    client.queryPayment('ORD123'),
    client.queryPayment('ORD456')
  ]);
  
  console.log('用户信息:', user);
  console.log('订单1:', payment1);
  console.log('订单2:', payment2);
}
```

### 5. 如何启用调试模式？

```javascript
const client = new OpenForAllClient({
  ...config,
  debug: true,
  logger: console  // 使用自定义logger
});
```

---

## 🤝 贡献指南

我们欢迎所有形式的贡献！

### 如何贡献

1. **Fork** 本仓库
2. **创建** 特性分支 (`git checkout -b feature/AmazingFeature`)
3. **提交** 更改 (`git commit -m 'Add some AmazingFeature'`)
4. **推送** 到分支 (`git push origin feature/AmazingFeature`)
5. **提交** Pull Request

### 开发环境设置

```bash
# 克隆仓库
git clone https://github.com/openforall/wechat-sdk-nodejs.git
cd wechat-sdk-nodejs

# 安装依赖
npm install

# 运行测试
npm test

# 构建
npm run build

# 代码格式化
npm run lint
npm run format
```

### 代码规范

- 遵循 [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- 使用 ESLint 和 Prettier
- 编写 JSDoc 注释
- 添加单元测试

---

## 📞 技术支持

### 获取帮助

- 📖 **文档中心**: https://openforall.liebianjun.com/docs
- 💬 **问题反馈**: [GitHub Issues](https://github.com/openforall/wechat-sdk-nodejs/issues)
- 📧 **邮件支持**: support@openforall.com
- 💼 **商务合作**: business@openforall.com

### 社区交流

- 🐛 **Bug反馈**: [提交Issue](https://github.com/openforall/wechat-sdk-nodejs/issues/new)
- 💡 **功能建议**: [功能请求](https://github.com/openforall/wechat-sdk-nodejs/issues/new?labels=enhancement)
- 📚 **技术博客**: [CSDN](https://blog.csdn.net/openforall) | [掘金](https://juejin.cn/user/openforall)

---

## 🌟 相关项目

### 官方SDK

- 🐘 **PHP SDK**: [openforall/wechat-sdk-php](https://github.com/openforall/wechat-sdk-php)
- 🐍 **Python SDK**: [openforall/wechat-sdk-python](https://github.com/openforall/wechat-sdk-python)
- ☕ **Java SDK**: [openforall/wechat-sdk-java](https://github.com/openforall/wechat-sdk-java)

### 框架集成

- ⚡ **Express**: [openforall/express-wechat](https://github.com/openforall/express-wechat)
- 🚀 **Koa**: [openforall/koa-wechat](https://github.com/openforall/koa-wechat)
- 🔥 **Nest.js**: [openforall/nestjs-wechat](https://github.com/openforall/nestjs-wechat)

---

## 📄 开源协议

本项目采用 [MIT License](LICENSE) 开源协议。

---

## 📈 项目统计

![NPM Downloads](https://img.shields.io/npm/dm/openforall-sdk)
![GitHub stars](https://img.shields.io/github/stars/openforall/wechat-sdk-nodejs?style=social)
![GitHub forks](https://img.shields.io/github/forks/openforall/wechat-sdk-nodejs?style=social)

---

<div align="center">

**⭐ 如果这个项目对您有帮助，请给我们一个Star！⭐**

Made with ❤️ by [OpenForAll Team](https://openforall.liebianjun.com)

[官网](https://openforall.liebianjun.com) • [文档](https://openforall.liebianjun.com/docs) • [NPM](https://www.npmjs.com/package/openforall-sdk) • [博客](https://blog.openforall.com)

</div>
