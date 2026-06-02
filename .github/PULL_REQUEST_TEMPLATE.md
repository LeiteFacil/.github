<!-- Título do PR seguindo Conventional Commits, ex.: feat: ... / fix: ... -->

## 📋 O que este PR faz

<!-- Descreva O QUÊ e POR QUÊ. O "como" o reviewer lê no diff. -->

## 🔗 Contexto / Issue relacionada

<!-- Closes #123 / link da task no ClickUp / contexto -->

## 🧪 Como testar

<!-- Passos para validar localmente -->
1.
2.

## 🌐 Impacto entre serviços

<!-- Marque se este PR muda contrato de API ou afeta outros repos -->
- [ ] Não afeta outros serviços
- [ ] Afeta o **front** / **mobile** (contrato de API atualizado nos dois lados)
- [ ] Afeta o **Agro-Core / IdP** (`/internal/*`)
- [ ] Requer **migração** de banco (Drizzle)
- [ ] Requer atualização de variáveis de ambiente

## ✅ Checklist

- [ ] `lint` passou sem warnings (`--max-warnings 0`)
- [ ] `typecheck` / `tsc` passou
- [ ] Testes unitários passaram; E2E rodado se cruza serviços
- [ ] Sem resíduo legacy (código/schema antigo removido)
- [ ] Front alinhado ao contrato do **back** (back é a fonte da verdade)
- [ ] Sem segredos commitados (`.env`, chaves, tokens)
- [ ] Sem assinatura automática de IA no commit
