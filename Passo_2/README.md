### Prisma Database

Sobre os arquivos base necessarios, arquivos padrões

```
|-src/
   |-prisma/
        |-prisma.module.ts
        |-prisma.service.ts
```

#### prisma.module.ts

```Typescript
/* eslint-disable prettier/prettier */
import { Module } from '@nestjs/common';
import { PrismaService } from './prisma.service';

@Module({
  providers: [PrismaService],
  exports: [PrismaService],
})
export class PrismaModule {}
```

#### prisma.service.ts

```Typescript
/* eslint-disable prettier/prettier */
import { Injectable, OnModuleDestroy, OnModuleInit } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService
  extends PrismaClient
  implements OnModuleInit, OnModuleDestroy
{
  async onModuleInit() {
    await this.$connect();

    // Adiciona um listener para o evento 'beforeExit'
    process.on('beforeExit', async () => {
      await this.onModuleDestroy();
      process.exit(0);
    });
  }

  async onModuleDestroy() {
    await this.$disconnect();
  }
}
```

Voltar para a [pagina inicial](/README.md)
