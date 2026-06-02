<div align="center">

<img src="https://raw.githubusercontent.com/LeiteFacil/.github/main/profile/assets/mascote.svg" alt="Leite Fácil" width="150" />

# Leite Fácil

### Plataforma de gestão pecuária leiteira — do campo ao financeiro

*Manejo de rebanho · reprodução (IATF) · sanidade · produção leiteira · coleiras IoT · faturamento*

<br/>

![Status](https://img.shields.io/badge/status-em%20produção-2ea44f?style=for-the-badge)
![Plataforma](https://img.shields.io/badge/web%20·%20mobile%20·%20IoT-multiplataforma-1f6feb?style=for-the-badge)
![Repos](https://img.shields.io/badge/código-privado-6e7681?style=for-the-badge)

<br/>

![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Expo](https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white)
![Drizzle](https://img.shields.io/badge/Drizzle_ORM-C5F74F?style=flat-square&logo=drizzle&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![OAuth2](https://img.shields.io/badge/OAuth_2.0_·_RS256-EB5424?style=flat-square&logo=auth0&logoColor=white)

</div>

---

## Sobre

O **Leite Fácil** é uma plataforma SaaS para produtores e veterinários gerenciarem a
operação leiteira de ponta a ponta: cadastro e manejo de animais, protocolos de
inseminação (**IATF**), controle sanitário, registro de produção, dietas, relatórios
analíticos, coleiras IoT de monitoramento e o ciclo financeiro (assinaturas e cobrança).

A arquitetura é composta por serviços independentes que conversam entre si através de um
**BFF** central, com identidade e autenticação isoladas em um **Identity Provider** próprio.

---

## Arquitetura

```mermaid
flowchart TD
    subgraph Clientes
        FE["Front-end Web<br/>React + Vite"]
        MO["App Mobile<br/>Expo · offline-first"]
        ADM["Painel ADM<br/>React"]
    end

    subgraph Backends
        BFF["Back-end / BFF<br/>NestJS · :3001<br/>domínio + orquestração"]
        ADMB["ADM Back-end<br/>NestJS"]
        CORE["Agro-Core (IdP)<br/>NestJS · :3000<br/>auth · users · /internal/*"]
    end

    subgraph Infra
        DB[("PostgreSQL<br/>Drizzle ORM")]
        IOT["Coleiras IoT"]
    end

    FE -->|auth via BFF| BFF
    MO -->|REST| BFF
    ADM --> ADMB
    BFF -->|OAuth2 RS256| CORE
    ADMB --> CORE
    BFF --> DB
    ADMB --> DB
    CORE --> DB
    IOT --> BFF
```

> A autenticação do front passa **pelo BFF (`:3001`)**; o **Agro-Core** expõe apenas
> rotas `/internal/*` para os back-ends, nunca diretamente para os clientes.

---

## Serviços

| Repositório | Papel | Stack |
|---|---|---|
| **`Agro-Core`** | Identity Provider standalone — auth, identidade e *user management* (`:3000`) | NestJS · BullMQ · class-validator |
| **`leite-facil-back-end`** | Back-end de domínio + BFF — regra de negócio e orquestração (`:3001`) | NestJS · Drizzle ORM · PostgreSQL |
| **`leite-facil-front-end`** | Aplicação web principal do produtor/veterinário | React · Vite · TanStack Query · Sentry |
| **`leite-facil-mobile`** | App de campo offline-first (sincronização automática) | Expo · React Native · TanStack Query |
| **`leite-facil-adm-back-end`** | Back-end do painel administrativo | NestJS · Drizzle · Neon |
| **`leite-facil-adm-front-end`** | Painel administrativo (gestão interna) | React · React Router · Tailwind |
| **`leite-facil-coleiras`** | Integração das coleiras IoT de monitoramento | — |
| **`leite-facil-e2e`** | Testes end-to-end do ecossistema | Node · pg |

---

## Stack & padrões

| Camada | Tecnologias |
|---|---|
| **Back-end** | NestJS · TypeScript · Drizzle ORM · PostgreSQL · BullMQ |
| **Front-end** | React · Vite · TanStack Query · Tailwind · Radix UI · Hugeicons |
| **Mobile** | Expo · React Native · AsyncStorage (offline-first) |
| **Auth** | OAuth 2.0 · JWT RS256 (public key) · class-validator |
| **Observabilidade** | Sentry |
| **Qualidade** | ESLint (`--max-warnings 0`) · Husky · lint-staged · testes E2E |

**Convenções do ecossistema**

- Autenticação via **OAuth 2.0 / JWT RS256**, validação com **class-validator** (não Zod).
- Em conflitos de contrato front × back, **o back é a fonte da verdade**.
- Sem resíduo legacy: migrações e refatorações são feitas de uma vez (com backup).
- Pre-commit roda **lint-staged + ESLint sem tolerância a warnings**.

---

## Áreas do produto

![Rebanho](https://img.shields.io/badge/Manejo_de_rebanho-1f6feb?style=flat-square)
![IATF](https://img.shields.io/badge/Reprodução_·_IATF-1f6feb?style=flat-square)
![Sanidade](https://img.shields.io/badge/Sanidade_·_diagnósticos-1f6feb?style=flat-square)
![Produção](https://img.shields.io/badge/Produção_leiteira-1f6feb?style=flat-square)
![Dietas](https://img.shields.io/badge/Dietas_·_nutrição-1f6feb?style=flat-square)
![Relatórios](https://img.shields.io/badge/Relatórios-1f6feb?style=flat-square)
![IoT](https://img.shields.io/badge/Coleiras_IoT-1f6feb?style=flat-square)
![Faturamento](https://img.shields.io/badge/Faturamento_·_assinaturas-1f6feb?style=flat-square)

---

<div align="center">

### Repositórios internos

Este é o perfil da organização **Leite Fácil**. O código é privado — acesso restrito à equipe.

<sub>Feito para o campo · © Leite Fácil</sub>

</div>
