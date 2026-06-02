# Contribuindo com o Leite Fácil

Obrigado por contribuir! Este guia vale para **todos os repositórios** da organização
(é um *default community health file* hospedado em `.github`). Cada repo pode
sobrescrever com seu próprio `CONTRIBUTING.md`.

---

## 🧭 Princípios do ecossistema

- **O back-end é a fonte da verdade.** Em conflitos de contrato front × back, o front
  se alinha ao back — nunca o contrário.
- **Sem resíduo legacy.** Migrações e refatorações são feitas de uma vez (com backup),
  sem manter código/schema antigo coexistindo.
- **Auth padronizada.** OAuth 2.0 com JWT **RS256** (validação por public key) e
  **class-validator** nos DTOs (não usamos Zod no back).
- **Identidade isolada.** O `Agro-Core` (IdP, `:3000`) só expõe `/internal/*` para os
  back-ends. O front autentica **via BFF** (`leite-facil-back-end`, `:3001`).

---

## 🛠️ Setup local

```bash
# instale as dependências (use o gerenciador do repo: pnpm ou npm)
pnpm install        # ou: npm install

# copie e ajuste as variáveis de ambiente
cp .env.example .env
```

> O **mobile** usa `pnpm` com `node-linker=hoisted`. O **front** consome o BFF via
> `VITE_AUTH_BASE_URL`. Confira o `README.md` de cada repositório para portas e envs.

---

## 🌿 Fluxo de trabalho

1. Crie uma branch a partir da branch de integração do repo:
   ```bash
   git checkout -b feat/minha-feature
   ```
2. Faça commits pequenos e descritivos seguindo **Conventional Commits**:
   ```
   feat: adiciona protocolo IATF event-driven
   fix: corrige mismatch de health-status EN×PT no BFF
   refactor: extrai coverage_period para módulo dedicado
   chore: bump de dependências
   ```
3. Abra um **Pull Request** preenchendo o template.
4. Garanta que **CI, lint e testes** estão verdes antes de pedir review.

### Regras de commit

- ❌ **Não** adicione assinaturas automáticas (ex.: `Co-Authored-By`) gerada por IA.
- ❌ **Não** commite arquivos locais de ferramentas (ex.: `CLAUDE.md`, `.env`).
- ❌ **Não** faça `force-push` em branches compartilhadas.

---

## ✅ Qualidade — antes de abrir o PR

O pre-commit roda **lint-staged + ESLint sem tolerância a warnings**
(`--max-warnings 0`). Tocar num arquivo com warnings pré-existentes trava o commit,
então rode antes:

```bash
pnpm lint          # ESLint
pnpm typecheck     # tsc --noEmit (quando disponível)
pnpm test          # testes unitários
```

Para mudanças que cruzam serviços, rode também os testes **E2E**
(`leite-facil-e2e`).

> ⚠️ O `Agro-Core` é dependência cruzada (`file:../agro-core`) dos back-ends e
> **case-sensitive no Linux** (CI/Docker/Vercel/Render). Confira os imports.

---

## 🔍 Code review

- PRs precisam de pelo menos **1 aprovação**.
- Descreva **o quê** e **por quê**; o *como* o reviewer lê no diff.
- Mudanças que afetam contrato de API exigem atualização do front/mobile correspondente.

---

## 🔐 Segurança

Encontrou uma vulnerabilidade? **Não abra issue pública.** Siga o
[`SECURITY.md`](./SECURITY.md).
