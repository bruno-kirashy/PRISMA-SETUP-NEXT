# 🚀 Guia de Configuração Prisma com Next.js

> 📘 Guia completo passo a passo para configurar o Prisma ORM em projetos Next.js, incluindo configuração de migrations, seeds e boas práticas para evitar múltiplas conexões com o banco de dados.

## 📋 O que você vai encontrar neste guia

- ✅ Instalação e configuração inicial do Prisma
- ✅ Configuração do arquivo `.env` e `schema.prisma`
- ✅ Setup de migrations para controle de versão do banco
- ✅ Configuração de seeds para popular o banco com dados iniciais
- ✅ Solução de problemas comuns de configuração
- ✅ Boas práticas para conexão com banco de dados no Next.js

---

## 📦 Primeiros comandos
```bash
npm i axios zustand
```

## ⚙️ Configuração do Prisma

### 🔧 Instalação inicial
```bash
npm i -D prisma
npx prisma init
```

### ⚠️ Caso der erro

Instalar o dotenv:
```bash
# Com npm
npm install dotenv
```

Dar import do dotenv no arquivo `prisma.config.ts`, porque `prisma.config.ts` toma a frente do `.env`:
```typescript
import "dotenv/config";
```

### 🔐 Configurar .env

Trocar a URL do banco de dados:
```env
DATABASE_URL=postgresql://janedoe:mypassword@localhost:5432/mydb
```

### 📝 Configurar schema.prisma

No `schema.prisma` altere:
```prisma
generator client {
  provider = "prisma-client"
  output   = "../app/generated/prisma"
}
```

Para:
```prisma
generator client {
  provider = "prisma-client-js"
  output   = "../app/generated/prisma"
}
```

Após isso crie o banco de dados nesse arquivo, e prossiga.

### 🗃️ Criar migration

Depois de criado, dê o comando e dê o nome da estrutura inicial do seu banco de dados:
```bash
npx prisma migrate dev
```

## 🔌 Configurar conexão com o banco

Crie uma pasta chamada `lib` e dentro dela o arquivo `prisma.ts`, e o comando para não gerar várias conexões com o banco, fornecido na documentação do Prisma:

[https://www.prisma.io/docs/orm/more/help-and-troubleshooting/nextjs-help](https://www.prisma.io/docs/orm/more/help-and-troubleshooting/nextjs-help)

### 💾 Instalar Prisma Client
```bash
npm install prisma @prisma/client
```

## 🌱 Configurar Seed

Crie o `seed.ts` do projeto, na pasta `prisma`, e vá até o `package.json` e adicione o comando para o Next.js:
```json
"prisma": {
  "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts"
}
```

### 📥 Instalar ts-node

Instale o ts-node para conseguir executar o comando do seed:
```bash
npm i -D ts-node
```

### ▶️ Executar seed

Agora dê o comando:
```bash
npx prisma db seed
```

---

## 🎯 Próximos passos

Após concluir este setup, você está pronto para:
- Criar seus models no `schema.prisma`
- Executar migrations com `npx prisma migrate dev`
- Utilizar o Prisma Client em suas rotas e componentes
- Popular o banco com dados iniciais através do seed

## 📚 Recursos úteis

- [Documentação oficial do Prisma](https://www.prisma.io/docs)
- [Prisma + Next.js](https://www.prisma.io/docs/orm/more/help-and-troubleshooting/nextjs-help)
- [Prisma Schema Reference](https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference)

---

✨ **Pronto! Seu Prisma está configurado e pronto para uso!** ✨
