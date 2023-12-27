### Prisma Database

![img](/imageReadme/imageREADME.png)

### Prisma Database exemplo service

```Typescript
// Importa o decorador Injectable do NestJS para tornar a classe um serviço injetável.
import { Injectable } from '@nestjs/common';

// Importa o serviço Prisma para realizar operações no banco de dados.
import { PrismaService } from '../prisma/prisma.service';

// Adiciona o decorador Injectable para marcar a classe como um serviço injetável no contexto do NestJS.
@Injectable()
export class UserService {
  // Define o construtor da classe e injeta o serviço Prisma.
  constructor(private prisma: PrismaService) {}

  // Método assíncrono para criar um novo usuário no banco de dados.
  async createUser(name: string, password: string) {
    // Utiliza o Prisma para criar um novo usuário com os dados fornecidos.
    return this.prisma.user.create({
      data: {
        name,
        password,
      },
    });
  }

  // Método assíncrono para obter todos os usuários do banco de dados.
  async getAllUsers() {
    // Utiliza o Prisma para buscar todos os usuários.
    return this.prisma.user.findMany();
  }

  // Método assíncrono para obter um usuário pelo ID.
  async getUserById(id: number) {
    // Utiliza o Prisma para buscar um usuário específico pelo ID.
    return this.prisma.user.findUnique({
      where: { id },
    });
  }

  // Método assíncrono para atualizar um usuário no banco de dados.
  async updateUser(id: number, name: string, password: string) {
    // Utiliza o Prisma para atualizar um usuário com os dados fornecidos.
    return this.prisma.user.update({
      where: { id },
      data: { name, password },
    });
  }

  // Método assíncrono para excluir um usuário do banco de dados.
  async deleteUser(id: number) {
    // Utiliza o Prisma para excluir um usuário específico pelo ID.
    return this.prisma.user.delete({
      where: { id },
    });
  }
}

```
