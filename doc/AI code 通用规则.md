## 后端（`backend`）

### 技术栈

- **语言/框架**：Go 1.26、Gin
- **数据库**：PostgreSQL 14，通过 GORM 访问（snake_case、UUID 主键、`deleted_at` 软删除）
- **认证**：JWT
- **接口文档**：Swag

### 接口设计规范

- **HTTP 方法**：所有接口统一使用 `POST`，不在路径中携带参数（`id`、`code` 等标识符放入请求体）。仅文件二进制下载接口使用 `GET`。
- 列表响应格式：`{ "list": [], "pagination": { "page", "pageSize", "total" } }`
- 状态切换接口：`POST /{resource}/status`（`id` 放请求体）
- 权限码格式：`resource:action`（例如 `platform-user:view`）

## 数据库规范

- 主键：统一使用 `id uuid`
- 外键字段：`xxx_id`；编码引用：`xxx_code`
- 每张表必须有审计字段：`created_at`、`created_by`、`updated_at`、`updated_by`（软删除表额外加 `deleted_at`）
- 密码存储为 `password_hash`，禁止明文

## 前端（`frontend`）

### 技术栈

- **包管理器**：pnpm workspace
- **公共技术栈**：TypeScript、Rsbuild、React、Tailwind CSS v4、Zustand、TanStack Router、TanStack Query、ECharts、Vitest、Biome、openapi-typescript

### 前端页面规范 

- 所有列表必须处理：空状态、加载中、接口报错、无权限
- 高风险操作（删除、重置密码、发布消息）需二次确认弹窗
- 表单提交失败时须保留已填内容

### 通用目录规范
```
- `src/main.tsx`：应用入口与 Provider 挂载
- `src/router.tsx`：路由树、守卫、重定向逻辑
- `src/index.css`：全局样式入口
- `src/layouts/`：应用级布局壳层，如顶栏、侧栏、主框架
- `src/components/common/`：跨页面复用的通用组件
- `src/routes/`：路由页面，按业务域分组
- `src/stores/`：前端状态管理
- `src/services/`：面向业务域的接口调用与流程编排
- `src/utils/`：纯工具函数、类型辅助、底层请求封装
```

## 语言规范

- 代码注释、文档、页面显示文字、git commit 信息，均使用**简体中文**。
- 生成代码时，对函数、关键逻辑、复杂算法、业务规则等适当添加中文注释，帮助理解意图；简单赋值或显而易见的代码无需注释。
