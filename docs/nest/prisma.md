# prisma

```shell
# 初始化 prisma 目录结构
npx prisma init
# 自动识别 schema 生成外键等声明
npx prisma format
# 生成迁移文件、数据库更新、生成 PrismaClient
npx prisma migrate dev
# 运行数据填充脚本
npx prisma db seed
# 重置数据库并填充数据
npx prisma migrate reset
```

## Getting Start

Prisma 可以方便的管理数据表，包含数据迁移、数据填充、查询生成器等好用的功能。

### 安装依赖

安装 Prisma CLI 等扩展包

- 使用[mockjs (opens new window)](http://mockjs.com/examples.html)生成随机数据
- 使用 [argon2 (opens new window)](https://www.npmjs.com/package/argon2)加密密码

安装所需的包

```shell
pnpm add prisma-binding @prisma/client mockjs argon2
pnpm add -D prisma typescript @types/node @types/mockjs
```

### 数据库连接

执行以上命令后初始化 prisma

```shell
npx prisma init
```

会创建`.env`文件与`prisma`文件夹

- .env 用于定义数据库连接
- prisma 用于定义模型结构与数据迁移与数据填充文件

修改`.env`文件设置 mysql 连接，以下连接请根据情况修改

```shell
DATABASE_URL="mysql://root:admin888@127.0.0.1:3306/nest"
```

## 迁移文件

迁移文件 migrate 用于构建数据表结构变化，他是数据库的**版本控制**机制，每次表结构的修改都有单独文件记录。

### 结构定义

在 `prisman/schema.prisma` 文件内定义表结构:

> 你可以查看[数据模型 (opens new window)](https://prisma.yoga/concepts/components/prisma-schema/data-model#定义属性)或 [字段类型 (opens new window)](https://prisma.yoga/reference/api-reference/prisma-schema-reference#model-字段)文档了解使用方法。

```text
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}

model user {
  // BigInt类型	主键 自增值	非负BitInt
  id       BigInt    @id @default(autoincrement()) @db.UnsignedBigInt()
  // 字符串，默认为varchar(191)
  email    String
  password String
  // 添加时自动设置时间，即设置Mysql默认值为CURRENT_TIMESTAMP
  createdAt DateTime @default(now())
  // 让Prisma在添加与更新时自动维护该字段
  updatedAt DateTime @updatedAt
}

model category {
  id       Int       @id @default(autoincrement()) @db.UnsignedInt()
  title    String
  articles article[]
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt
}

model article {
  id         Int      @id @default(autoincrement()) @db.UnsignedInt()
  title      String
  content    String   @db.Text()
  // 类型category	关联定义(本表字段catgoryId,关联category表id,主表记录删除时同时删除关联表数据）
  // 通过 vicode prisma插件自动生成，或者 npm prisma format
  category   category @relation(fields: [categoryId], references: [id], onDelete: Cascade)
  categoryId Int      @db.UnsignedInt()
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt
}
```

执行以下命令，将自动根据已经存在的数据库生成文件 `prisman/schema.prisma` ，而不需要向上面一样手动定义。

```shell
npx prisma db pull
```

### 生成迁移

当创建好结构定义后，执行以下命令会在`prisma/migrations` 目录生成迁移文件，同时在数据库中创建表。

- 这时数据表也已经创建了
- 数据库中会有表 `_prisma_migrations` 记录了迁移文件

```shell
npx prisma migrate dev
```

✅ 以下命令执行动作为：

- 根据定义生成迁移文件
- 执行新的迁移文件修改数据表
- 生成 **Prisma Client**

### 重置数据库

我们也可以执行以下命令重置数据库

```shell
npm prisma migrate reset
```

以下命令执行动作为：

- 删除数据库
- 创建数据库
- 执行所有迁移文件
- 运行 seed 数据填充

## 查询构造器

当执行 prisma migrate dev 后，系统会生成针对于每个表的查询构建器 `PrismaClient`。

- 查询构造器提供众多方法完成对数据的增删改查
- 你可以查看文档 [prisma-client (opens new window)](https://prisma.yoga/concepts/components/prisma-client)了解详细使用

下面在中创建文件`test.ts`，用于测试查询构造器，内容如下

```typescript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

Promise.resolve().then(async () => {
  const user = await prisma.user.findFirst();
  console.log(user);
});
```

需要安装以下命令完成测试

```shell
pnpm add -g nodemon ts-node
```

然后执行命令查看结果

```shell
nodemon test.ts
```

## 数据填充

[数据填充 (opens new window)](https://prisma.yoga/guides/database/seed-database)一般用于在开发时添加测试数据，我们会使用 prisma 的 [prisma-client (opens new window)](https://prisma.yoga/concepts/components/prisma-client)查询构造器进入数据添加。

### 环境配置

同时为了生成随机数据需要安装 [mockjs (opens new window)](http://mockjs.com/)。

```shell
pnpm add mockjs
```

首先在 package.json 中定义命令，后面可以调用 `npx prisma db seed` 命令实现填充

```json
{
  "name": "nest",
  "prisma": {
    "seed": "ts-node prisma/seed.ts"
  }
}
```

然后你需要创建`prisma/seeds`目录 ，该目录用于定义数据填充文件。

### 代码逻辑

创建帮助函数 `prisma/helper.ts`，并实现 create 方法用于批量执行填充动作。

```typescript
export default async function create(
  count = 10,
  callback: () => Promise<void>
) {
  const prisma = new PrismaClient();
  for (let i = 1; i <= count; i++) {
    await callback(prisma);
  }
}
```

接着定义`seeds/user.ts`文件用于定义 user 表的数据

```typescript
import { PrismaClient } from "@prisma/client";
import { Random } from "mockjs";
import { hash } from "argon2";
import create from "../helper";

export default () => {
  create(10, async (prisma: PrismaClient) => {
    await prisma.user.create({
      data: {
        email: Random.email(),
        password: await hash(Random.sentence()),
      },
    });
  });
};
```

然后创建文件 prisma/seed.ts ，这个文件是执行`npx prisma db seed`命令时调用的

> 因为有些表需要其他表先创建，所以定义 bootstrap 方法，使用 await 让他们按顺序执行

```typescript
import { UserSeed } from "./seeds/user";

function run() {
  UserSeed(10);
}

run();
```

### 填充命令

✅ 现在执行命令就可以有填充数据了

```typescript
npx prisma db seed
```

✅ 执行以下命令会自动执行数据填充

```typescript
npx prisma migrate reset
```

### 外键约束

如果数据表有外键依赖时，需要保证被依赖的表先创建。这时需要使用**await** 函数阻塞异步执行。

首先修改 **seed.ts** 文件，让调用的填充文件阻塞执行

```typescript
import { UserSeed } from "./seeds/user";

async function run() {
  await UserSeed(10);
}

run();
```

接着修改 **UserSeed.ts** 文件，将函数定义为 **async/await**

```typescript
...
export default async() => {
	await create(10, async (prisma:PrismaClient) => {
    await prisma.user.create({
      data: {
        email: Random.email(),
        password: await hash(Random.sentence()),
      },
    });
  });
};
```

## 常用命令

创建迁移文件

```shell
npm prisma migrate dev
```

重置迁移并执行数据，同时会执行数据填充

```shell
npm prisma migrate reset
```

执行数据填充

```shell
npm prisma db seed
```

## 定义模块

下面我们在项目代码中使用 prisma，首先创建 prisma 模块。

```text
nest g mo prisma
nest g s prisma
```

### 提供者/LOG

创建 **prisma/prisma.service.ts** 服务文件，同时将在文件中定义 [日志记录 (opens new window)](https://prisma.yoga/concepts/components/prisma-client/working-with-prismaclient/logging)。

> 当为开发环境时，终端输入查询 SQL

```typescript
import { Injectable } from "@nestjs/common";
import { ConfigService } from "@nestjs/config";
import { PrismaClient } from "@prisma/client";

@Injectable()
export class PrismaService extends PrismaClient {
  constructor(configService: ConfigService) {
    //输出查询SQL等LOG
    super(
      configService.get("app.isDev")
        ? { log: ["query", "info", "warn", "error"] }
        : undefined
    );
  }
}
```

然后设置模块 **prisma/prisma.module.ts** 注册提供者，并使用 exports 选项向外部提供 **PrismaService** 服务

```typescript
import { Global, Module } from "@nestjs/common";
import { PrismaService } from "./prisma.service";

@Global()
@Module({
  providers: [PrismaService],
  exports: [PrismaService],
})
export class PrismaModule {}
```

然后在根模块 **app.module.ts** 中注册

```typescript
import { PrismaModule } from "./prisma/prisma.module";
import { Module } from "@nestjs/common";
import { AppController } from "./app.controller";
import { AppService } from "./app.service";
import { UserModule } from "./user/user.module";
import { AuthModule } from "./auth/auth.module";

@Module({
  imports: [UserModule, AuthModule, PrismaModule],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

### 使用

现在其他模块也可以使用 **PrismaService** 服务了

> 因为 prisma 模块已经注册全局，所以其他模块不需要 import

```typescript
import { PrismaService } from './../prisma/prisma.service';
import { Injectable, ForbiddenException } from '@nestjs/common';
import { CreateAuthDto } from './dto/create-auth.dto';
import * as argon2 from 'argon2';

@Injectable()
export class AuthService {
  constructor(private readonly prisma: PrismaService) {}
  ...
}
```

## 常见问题

1. 当 prisma 出错异常时，你可以删除 prisma 迁移文件

   你可以删除数据库所有表，和项目中的 `prisma/migrations` 目录，将 prisma 初始到最干净的状态
