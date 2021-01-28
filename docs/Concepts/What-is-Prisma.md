---
lastAuthor: Leo-Ryu
lastEdited: 1611810121891
---
# What is Prisma

\
Prisma is an [open source](https://github.com/prisma/prisma) next-generation ORM. It consists of the following parts:

\
* **Prisma Client**: Auto-generated and type-safe query builder for Node.js & TypeScript
* **Prisma Migrate** (Preview): Migration system
* **Prisma Studio**: GUI to view and edit data in your database

  \

Prisma Client can be used in *any* Node.js (supported versions) or TypeScript backend application (including serverless applications and microservices). This can be a [REST API](https://www.prisma.io/docs/concepts/overview/prisma-in-your-stack/rest/), a [GraphQL API](https://www.prisma.io/docs/concepts/overview/prisma-in-your-stack/graphql/), a gRPC API, or anything else that needs a database.

\
## How does Prisma work?

### The Prisma schema

Every project that uses a tool from the Prisma toolkit starts with a [Prisma schema file](https://www.prisma.io/docs/concepts/components/prisma-schema/). The Prisma schema allows developers to define their *application models* in an intuitive data modeling language. It also contains the connection to a database and defines a *generator*:

\
```javascript
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
generator client {
  provider = "prisma-client-js"
}
model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  author    User?   @relation(fields:  [authorId], references: [id])
  authorId  Int?
}
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}
```

\
