# 💸 Gasto Claro

> Controle financeiro pessoal full-stack: registre receitas e despesas, defina orçamentos por categoria e entenda para onde o dinheiro vai com um dashboard mensal.

![Status](https://img.shields.io/badge/status-planejamento-blue)
![Angular](https://img.shields.io/badge/Angular-21-dd0031)
![NestJS](https://img.shields.io/badge/NestJS-API-e0234e)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-dados-336791)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178c6)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📑 Sumário

1. [Nome e Descrição](#1-nome-e-descrição)
2. [Objetivo e Problema Resolvido](#2-objetivo-e-problema-resolvido)
3. [Público-alvo](#3-público-alvo)
4. [Funcionalidades do MVP](#4-funcionalidades-do-mvp)
5. [Funcionalidades Futuras](#5-funcionalidades-futuras)
6. [Stack Tecnológica e Justificativas](#6-stack-tecnológica-e-justificativas)
7. [Arquitetura e Organização](#7-arquitetura-e-organização)
8. [Estrutura Inicial de Pastas](#8-estrutura-inicial-de-pastas)
9. [Plano de Desenvolvimento Passo a Passo](#9-plano-de-desenvolvimento-passo-a-passo)
10. [Boas Práticas e Padrões de Código](#10-boas-práticas-e-padrões-de-código)
11. [Desafios Técnicos e Conhecimentos Desenvolvidos](#11-desafios-técnicos-e-conhecimentos-desenvolvidos)
12. [Evolução Futura](#12-evolução-futura)

---

## 1. Nome e Descrição

**Gasto Claro** é uma aplicação web para controle financeiro pessoal. O usuário registra o que entra e o que sai, organiza tudo em categorias, define um limite mensal por categoria e acompanha o resultado em um dashboard com gráficos.

O projeto é **cliente-servidor clássico**, pensado como projeto de entrada:

- **Front-end (Angular):** formulários, listagem com filtros e paginação, dashboard com gráficos.
- **Back-end (NestJS + PostgreSQL):** autentica o usuário, guarda os dados, filtra, pagina e calcula os agregados (totais por categoria e por mês).

> **Diferença de um CRUD genérico:** o valor do projeto está nos **agregados** (consultas `GROUP BY`), nos **orçamentos com alerta**, nos **filtros combinados** sincronizados com a URL e no tratamento correto de **dinheiro**.

## 2. Objetivo e Problema Resolvido

### Problema
Muita gente chega ao fim do mês sem saber para onde o dinheiro foi. Planilhas exigem disciplina e não dão alertas; apps de banco mostram a lista, mas não o panorama.

### Objetivo
- **Registrar uma transação em poucos segundos.**
- **Enxergar o mês de relance:** quanto entrou, quanto saiu, quanto sobrou e onde foi gasto.
- **Ser avisado** antes de estourar o orçamento de uma categoria.
- **Exportar** os dados para uso em planilhas.

### Objetivo de aprendizado
Praticar no front-end **formulários reativos, filtros com RxJS, gráficos e rotas protegidas**; no back-end, **API autenticada, modelagem relacional, paginação, filtros dinâmicos e agregações SQL**.

## 3. Público-alvo

- **Jovens e estudantes** começando a organizar a vida financeira.
- **Estagiários e primeiro emprego**, com renda fixa e poucas categorias de gasto.
- **Recrutadores e desenvolvedores**, como vitrine de um app com dashboard, API e banco bem modelados.

## 4. Funcionalidades do MVP

### Front-end
| # | Funcionalidade | Descrição |
|---|---|---|
| 1 | **Cadastro e login** | Criar conta, entrar, sair e renovar a sessão automaticamente. |
| 2 | **Transações** | Criar, editar e excluir receitas e despesas (valor, data, categoria, descrição). |
| 3 | **Categorias** | Lista padrão criada no cadastro + categorias personalizadas (nome, cor). |
| 4 | **Listagem com filtros** | Período, tipo, categoria, texto e faixa de valor, combinados. |
| 5 | **Paginação e ordenação** | Navegação por páginas; ordenar por data ou valor. |
| 6 | **Filtros na URL** | Filtros refletidos na query string (link compartilhável, botão voltar funciona). |
| 7 | **Orçamento mensal** | Limite por categoria, com barra de progresso e estados (ok, atenção, estourado). |
| 8 | **Dashboard do mês** | Cards (receitas, despesas, saldo), gráfico por categoria e gráfico mensal. |
| 9 | **Navegação entre meses** | Troca de mês no dashboard e nos orçamentos. |
| 10 | **Exportar CSV** | Baixa as transações do filtro atual. |
| 11 | **Responsivo e tema** | Funciona bem no celular; tema claro e escuro. |
| 12 | **Estados de tela** | Carregando, vazio e erro tratados em todas as telas. |

### Back-end
| # | Funcionalidade | Descrição |
|---|---|---|
| 13 | **Autenticação** | Cadastro, login, access token de vida curta e refresh token. |
| 14 | **API de transações** | CRUD com filtros dinâmicos, ordenação e paginação, sempre isolado por usuário. |
| 15 | **API de categorias** | CRUD; não permite excluir categoria em uso (ou exige reatribuição). |
| 16 | **API de orçamentos** | Um limite por categoria por mês. |
| 17 | **Endpoints de resumo** | Totais do mês, gastos por categoria e série dos últimos N meses. |
| 18 | **Exportação CSV** | Gera o arquivo a partir dos mesmos filtros da listagem. |
| 19 | **Documentação da API** | Especificação OpenAPI navegável (Swagger). |

**Fora do MVP:** múltiplas contas/carteiras, importação de extrato, recorrências, metas de economia, compartilhamento entre usuários.

## 5. Funcionalidades Futuras

- Transações **recorrentes** (aluguel, assinaturas) geradas automaticamente.
- **Múltiplas contas** (carteira, banco, cartão) e transferências entre elas.
- **Parcelamento** de compras no cartão.
- **Importação** de CSV/OFX de extratos.
- **Metas de economia** com prazo e progresso.
- Anexar **comprovante** (upload de imagem).
- **Tags** além das categorias.
- Internacionalização (pt-BR, en) e múltiplas moedas.
- Relatório mensal em PDF.

## 6. Stack Tecnológica e Justificativas

| Camada | Tecnologia | Justificativa |
|---|---|---|
| Front | **Angular (estável atual) + TypeScript strict** | Formulários reativos robustos e estrutura opinativa. |
| Front | **Reactive Forms (tipados)** | Validação do formulário de transação e dos filtros. |
| Front | **Signals + serviços** | Estado simples e suficiente para o MVP; evita complexidade de store global. |
| Front | **RxJS** | Filtros com `debounceTime`, `distinctUntilChanged` e `switchMap`; interceptor de refresh de token. |
| Front | **Router (guards, query params)** | Rotas protegidas e filtros na URL. |
| Front | **Chart.js (via ng2-charts) ou ECharts** | Gráficos de pizza/rosca e de barras. |
| Front | **SCSS + CSS variables** | Tema claro/escuro e layout responsivo. |
| Back | **NestJS (TypeScript)** | Estrutura modular parecida com Angular; validação, guards e Swagger integrados. |
| Back | **PostgreSQL + TypeORM com migrations** | Dados relacionais, agregações SQL e schema versionado. |
| Back | **class-validator / class-transformer** | Validação dos DTOs de entrada. |
| Back | **JWT (access + refresh) + bcrypt/argon2** | Padrão para API stateless; senha com hash forte. |
| Back | **@nestjs/throttler** | Limite de requisições em login/cadastro. |
| Back | **@nestjs/swagger** | Contrato documentado. |
| Infra | **Docker Compose** | Banco e API reproduzíveis com um comando. |
| Qualidade | **Jest (front e back) + Supertest** | Regras de negócio, API e isolamento por usuário testados. |
| Qualidade | **ESLint + Prettier + CI** | Consistência e feedback automático. |

> **Decisão importante — dinheiro:** valores são guardados como **inteiros em centavos** (`amount_cents`, `bigint`) e trafegam assim na API. Nada de `number` com casas decimais: `0.1 + 0.2 !== 0.3`. O front converte para exibição (`Intl.NumberFormat`) e a máscara de entrada converte de volta para centavos.

> **Decisão — sem monorepo com pacotes compartilhados:** como projeto de entrada, `frontend/` e `backend/` são independentes. Os tipos da API são duplicados de forma consciente (ou gerados a partir do OpenAPI como evolução).

## 7. Arquitetura e Organização

### 7.1 Visão geral

```
┌────────────── FRONT-END (Angular) ──────────────┐
│ Páginas/Formulários → Serviços (Signals/RxJS)    │
│        │                    │                    │
│     Guards            HttpClient + Interceptors  │
│                       (token, refresh, erros)    │
└────────────────────────┬────────────────────────┘
                         │ HTTPS / JSON
                         ▼
┌────────────── BACK-END (NestJS) ────────────────┐
│ Controllers → Services → Repositories (TypeORM)  │
│   │ Guards (JWT)  │ DTOs/Pipes de validação      │
│                   ▼                              │
│              PostgreSQL                          │
└──────────────────────────────────────────────────┘
```

### 7.2 Comunicação Front ↔ Back
- API **REST em JSON**, prefixo `/api/v1`.
- Autenticação por header `Authorization: Bearer <accessToken>`.
- **Interceptor de autenticação** adiciona o token; ao receber `401`, tenta **uma** renovação com o refresh token e repete a requisição original. Se falhar, desloga.
- **Interceptor de erros** converte o formato padrão de erro da API em mensagens para o usuário.
- Datas trafegam como `YYYY-MM-DD` (data da transação, sem hora) e valores como **centavos inteiros**.
- **Erro padronizado:** `{ "statusCode": 400, "error": "Bad Request", "message": ["..."] }`.
- **CORS** liberado apenas para a origem do front-end.

### 7.3 Princípios
- **Controllers finos:** regras nos services; acesso a dados nos repositories.
- **Isolamento por usuário:** toda consulta filtra pelo `userId` do token; isso é **testado explicitamente**.
- **Agregação no banco:** totais por categoria e por mês via `SUM` + `GROUP BY`, não somando em memória.
- **Filtros como fonte de verdade na URL:** a tela lê os `queryParams`, não o contrário.
- **Componentes de apresentação separados dos de página**, com `OnPush`.
- **Dinheiro nunca é float.**

### 7.4 Autenticação e autorização
1. **Cadastro:** valida e-mail único, aplica hash na senha e cria as categorias padrão do usuário.
2. **Login:** devolve `accessToken` (≈15 min) e `refreshToken` (≈7 dias).
3. **Refresh token:** guardado **com hash** no banco; é **rotacionado** a cada uso e revogado no logout.
4. **Autorização:** um `JwtAuthGuard` global protege tudo, exceto rotas marcadas como públicas. Não há papéis: o modelo é "cada usuário só acessa o que é seu" (propriedade do recurso).
5. Recurso de outro usuário responde **404** (não revela existência).

### 7.5 Modelo de dados (inicial)

```
users                      categories
─────                      ──────────
id (uuid, PK)              id (uuid, PK)
name                       user_id (FK → users)
email (unique)             name
password_hash              color
created_at                 type  ('income' | 'expense')
                           created_at
                           UNIQUE (user_id, name, type)

transactions                         budgets
────────────                         ───────
id (uuid, PK)                        id (uuid, PK)
user_id (FK → users)                 user_id (FK → users)
category_id (FK → categories)        category_id (FK → categories)
type ('income' | 'expense')          month (date, sempre dia 1)
amount_cents (bigint, > 0)           limit_cents (bigint, > 0)
occurred_on (date)                   UNIQUE (user_id, category_id, month)
description (text, nullable)
created_at / updated_at              refresh_tokens
                                     ──────────────
Índices:                             id, user_id, token_hash,
 (user_id, occurred_on)              expires_at, revoked_at
 (user_id, category_id, occurred_on)
```

**Regras de integridade:**
- `amount_cents` sempre **positivo**; o sinal vem do `type`.
- O `type` da transação deve ser igual ao `type` da categoria.
- Categoria em uso não pode ser excluída sem reatribuição (`ON DELETE RESTRICT`).
- Orçamento só existe para categorias de despesa.

### 7.6 Contratos principais da API

Todas as rotas abaixo (exceto `auth/*` e `health`) exigem `Authorization: Bearer`.

| Recurso | Método e rota | Descrição |
|---|---|---|
| Auth | `POST /auth/register` | Cria conta. Body: `name`, `email`, `password`. |
| Auth | `POST /auth/login` | Retorna `accessToken` e `refreshToken`. |
| Auth | `POST /auth/refresh` | Troca o refresh token por um novo par. |
| Auth | `POST /auth/logout` | Revoga o refresh token. |
| Usuário | `GET /me` | Dados do usuário autenticado. |
| Categorias | `GET /categories` | Lista as categorias (`?type=`). |
| Categorias | `POST /categories` · `PATCH /categories/:id` · `DELETE /categories/:id` | CRUD. |
| Transações | `GET /transactions` | Lista com filtros e paginação (ver abaixo). |
| Transações | `POST /transactions` | Cria. |
| Transações | `GET /transactions/:id` · `PATCH` · `DELETE` | Leitura, edição e exclusão. |
| Transações | `GET /transactions/export.csv` | Exporta com os mesmos filtros da listagem. |
| Orçamentos | `GET /budgets?month=2026-11` | Orçamentos do mês com **gasto atual e percentual**. |
| Orçamentos | `PUT /budgets` | Cria ou atualiza o limite de uma categoria em um mês. |
| Orçamentos | `DELETE /budgets/:id` | Remove. |
| Resumo | `GET /summary/month?month=2026-11` | Receitas, despesas e saldo do mês. |
| Resumo | `GET /summary/by-category?month=2026-11&type=expense` | Total por categoria. |
| Resumo | `GET /summary/monthly?months=6` | Série de receitas e despesas dos últimos N meses. |
| Saúde | `GET /health` | Verificação de status. |

**Exemplo — listagem de transações**

```
GET /api/v1/transactions?from=2026-11-01&to=2026-11-30&type=expense
    &categoryId=<uuid>&q=mercado&minCents=1000&maxCents=50000
    &sort=occurredOn:desc&page=1&pageSize=20
```

```json
{
  "items": [
    {
      "id": "…",
      "type": "expense",
      "amountCents": 15990,
      "occurredOn": "2026-11-03",
      "description": "Mercado",
      "category": { "id": "…", "name": "Alimentação", "color": "#f97316" }
    }
  ],
  "page": 1,
  "pageSize": 20,
  "total": 87
}
```

**Exemplo — orçamento do mês**

```json
[
  {
    "id": "…",
    "category": { "id": "…", "name": "Lazer" },
    "month": "2026-11-01",
    "limitCents": 30000,
    "spentCents": 27500,
    "percent": 91.7,
    "status": "warning"
  }
]
```

Regra do `status`: `ok` (< 80%), `warning` (≥ 80% e < 100%), `exceeded` (≥ 100%).

## 8. Estrutura Inicial de Pastas

```
gasto-claro/
├── README.md
├── docker-compose                # PostgreSQL + API
├── .github/                      # CI: lint, testes, build
├── backend/
│   ├── .env.example
│   ├── migrations/
│   └── src/
│       ├── main
│       ├── config/               # variáveis de ambiente validadas
│       ├── common/               # guards, filtros de erro, decorators, paginação
│       └── modules/
│           ├── auth/
│           ├── users/
│           ├── categories/
│           ├── transactions/     # controller, service, dto, entity, query builder de filtros
│           ├── budgets/
│           ├── summary/          # agregações do dashboard
│           └── export/           # geração de CSV
└── frontend/
    └── src/
        ├── styles/               # tokens, tema claro/escuro
        └── app/
            ├── core/
            │   ├── auth/         # serviço, guard, interceptors
            │   ├── http/         # interceptor de erro, base da API
            │   └── services/     # tema, notificações
            ├── shared/           # componentes de UI, pipes (money, date), diretiva de máscara
            └── features/
                ├── auth/
                ├── transactions/ # lista, filtros, formulário
                ├── categories/
                ├── budgets/
                └── dashboard/    # cards e gráficos
```

## 9. Plano de Desenvolvimento Passo a Passo

Estimativa em ritmo parcial: **7 a 9 semanas**. Dica: **construa o back-end por fatias verticais** (um recurso completo, API + tela, antes do próximo).

### Fase 0 — Fundação (3 a 4 dias)
- [ ] Criar `frontend/` (Angular) e `backend/` (NestJS) com TypeScript strict.
- [ ] Configurar ESLint, Prettier, Jest e CI.
- [ ] Subir PostgreSQL com Docker Compose e configurar variáveis de ambiente validadas.
- [ ] Definir tokens de design (cores, espaçamento) e tema claro/escuro.

### Fase 1 — Autenticação (1 a 1,5 semana)
- [ ] Back: entidade `User`, cadastro, login, hash de senha, access e refresh token.
- [ ] Back: `JwtAuthGuard` global, rotas públicas, rate limiting no login.
- [ ] Front: telas de login/cadastro, guard de rota, interceptor com renovação de token.
- [ ] Testes: cadastro duplicado, senha errada, token expirado, refresh rotacionado.

### Fase 2 — Categorias (3 a 4 dias)
- [ ] Back: CRUD, categorias padrão criadas no cadastro, regra de exclusão.
- [ ] Front: tela de categorias com seletor de cor.
- [ ] Teste de isolamento: usuário B não vê nem altera categorias do usuário A.

### Fase 3 — Transações (2 semanas) — **núcleo do app**
- [ ] Back: migration, entidade, CRUD e validação (valor > 0, tipo compatível com a categoria).
- [ ] Back: filtros dinâmicos, ordenação e paginação em um único *query builder*.
- [ ] Front: formulário com máscara de moeda (centavos) e validações.
- [ ] Front: listagem com filtros reativos (`debounceTime`, `switchMap`) sincronizados com a URL.
- [ ] Front: estados de carregando, vazio e erro; confirmação de exclusão.
- [ ] Testes: combinações de filtros, paginação nos limites, isolamento por usuário.

### Fase 4 — Orçamentos (1 semana)
- [ ] Back: `PUT /budgets` idempotente e cálculo de gasto atual por categoria.
- [ ] Front: tela de orçamentos com barra de progresso e estados (ok, atenção, estourado).
- [ ] Testes do cálculo de `status` nos limites (79,9%, 80%, 100%).

### Fase 5 — Dashboard (1,5 semana)
- [ ] Back: endpoints de resumo com `SUM` + `GROUP BY` e índices adequados.
- [ ] Front: cards do mês, gráfico por categoria e gráfico dos últimos meses.
- [ ] Seletor de mês e tratamento de mês sem dados.
- [ ] Testes: totais corretos, mês vazio, fronteira entre meses (dia 1 e dia 30/31).

### Fase 6 — Exportação e acabamento (1 semana)
- [ ] CSV respeitando filtros, com escape correto de vírgulas e aspas e codificação UTF-8.
- [ ] Revisar acessibilidade, responsividade e performance.
- [ ] Documentação Swagger revisada.

### Fase 7 — Entrega (3 a 4 dias)
- [ ] Empacotar com Docker e publicar front e API em hospedagem gratuita.
- [ ] README final com capturas de tela, GIF e diagrama do modelo de dados.
- [ ] Teste ponta a ponta manual: cadastro → transações → orçamento estourado → dashboard → CSV.

## 10. Boas Práticas e Padrões de Código

**Geral**
- TypeScript strict, sem `any`.
- Commits pequenos (*Conventional Commits*); nomes no código em inglês.
- **Nunca** commitar segredos; usar `.env.example`.
- Uma branch por funcionalidade e *pull request* para si mesmo, descrevendo o que mudou e como testou.

**Front-end**
- Componentes *standalone*, `OnPush` e *lazy loading* por feature.
- Formulários tipados; lógica de filtro isolada em serviço, não no componente.
- Evitar `subscribe` manual em componentes: preferir `async` pipe, `toSignal` e `takeUntilDestroyed`.
- Formatação de moeda e data **apenas** em pipes compartilhados.
- Acessibilidade: `label` em todos os campos, foco visível, contraste, gráficos com alternativa em texto/tabela.

**Back-end**
- Validar toda entrada com DTOs; whitelist de propriedades.
- Respostas de erro padronizadas; não vazar detalhes internos.
- Migrations versionadas; nada de alterar o banco manualmente nem `synchronize: true`.
- **Toda consulta filtrada pelo usuário autenticado.**
- Ordenação aceita apenas campos de uma lista permitida (evita injeção por `sort`).
- Hash forte de senha; não registrar dados sensíveis em log.

**Testes e validação**
- **Unitários:** regras de negócio (cálculo de status do orçamento, validação tipo × categoria, montagem de filtros).
- **Integração/API (Supertest + banco de teste):** autenticação, CRUD, paginação, resumo e isolamento entre usuários.
- **Front:** testes de serviços, do formulário (validações e máscara) e do componente de filtros.
- **Critério de pronto de cada fatia:** funciona na tela, tem teste da regra principal, está documentado no Swagger e passa no CI.

## 11. Desafios Técnicos e Conhecimentos Desenvolvidos

| Desafio | O que você aprende |
|---|---|
| Dinheiro sem erro de arredondamento | Centavos inteiros, `Intl.NumberFormat`, máscara de entrada |
| Filtros combinados e dinâmicos | *Query builder*, índices, lista permitida de ordenação |
| Estado sincronizado com a URL | `ActivatedRoute`, `queryParams`, fonte única de verdade |
| Filtros reativos com RxJS | `debounceTime`, `distinctUntilChanged`, `switchMap` (cancela requisição antiga) |
| Agregações por categoria e mês | `SUM`, `GROUP BY`, `date_trunc`, fronteiras de mês |
| Gráficos de dados reais | Integração com biblioteca, estados vazios, acessibilidade |
| Autenticação com refresh de token | JWT, rotação de token, guards, interceptors |
| Isolamento entre usuários | Autorização por propriedade, testes de segurança |
| Paginação | Contrato `items/total/page`, limites e erros de uso |
| Docker e CI | Ambiente reproduzível e pipeline automatizado |

## 12. Evolução Futura

- **Recorrências** com tarefa agendada (`@nestjs/schedule`).
- **Múltiplas contas** e transferências.
- **Importação** de extratos CSV/OFX com pré-visualização e detecção de duplicatas.
- **Metas de economia** e projeção do saldo do mês.
- **Cache** de resumos (Redis), se a carga justificar.
- **Testes ponta a ponta** (Playwright): cadastro → lançamento → orçamento → dashboard.
- **Tipos gerados** a partir do OpenAPI para eliminar duplicação.
- **Recuperação de senha** por e-mail e login social.
- **PWA** para registrar gastos rapidamente pelo celular.

---

## 📝 Notas Finais

- Este documento é um **guia de planejamento**; ajuste o escopo ao seu ritmo.
- Entregue **uma fatia vertical por vez** (API + tela + teste): é assim que times trabalham.
- Ao fim de cada fase, atualize os checkboxes e registre o que aprendeu.
