# Migration `20200616161056-8`

This migration has been generated by Elias Bundala at 6/16/2020, 4:10:57 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "public"."Bid" ALTER COLUMN "state" SET DEFAULT E'PENDING';

ALTER TABLE "public"."Order" ALTER COLUMN "state" SET DEFAULT E'PENDING';

ALTER TABLE "public"."TokenOrder" ALTER COLUMN "state" SET DEFAULT E'PENDING';

ALTER TABLE "public"."Transaction" ALTER COLUMN "state" SET DEFAULT E'PENDING';

ALTER TABLE "public"."User" ADD COLUMN "disabled" boolean  NOT NULL DEFAULT true,
ALTER COLUMN "emailVerified" SET DEFAULT false,
ALTER COLUMN "role" SET DEFAULT E'USER';
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200616160254-7..20200616161056-8
--- datamodel.dml
+++ datamodel.dml
@@ -2,9 +2,9 @@
 // learn more about it in the docs: https://pris.ly/d/prisma-schema
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url      = env("DATABASE_URL")
 }
 generator client {
   provider = "prisma-client-js"
@@ -15,9 +15,10 @@
   uid           String       @unique
   email         String       @unique
   displayName   String
   phoneNumber   String       @unique
-  emailVerified Boolean
+  emailVerified Boolean      @default(false)
+  disabled      Boolean      @default(true)
   avator        File         @relation(fields: [avatorId], references: [id])
   avatorId      Int
   role          Role         @default(USER)
   expertise     Expertise[]
```

