# Política de Segurança — Leite Fácil

A segurança dos dados dos produtores e do rebanho é prioridade. Esta política vale
para todos os repositórios da organização.

## 📣 Reportando uma vulnerabilidade

**Não abra issues públicas para vulnerabilidades de segurança.**

Use um destes canais privados:

- 🔒 **GitHub Security Advisories** — aba **Security → Report a vulnerability** do
  repositório afetado (recomendado).
- 📧 **E-mail** — `leite.facil.app@gmail.com`.

Inclua, se possível:

- Descrição da vulnerabilidade e impacto potencial.
- Passos para reproduzir (PoC).
- Versão / branch / serviço afetado (`Agro-Core`, BFF, front, mobile, ADM…).

## ⏱️ O que esperar

| Etapa | Prazo alvo |
|---|---|
| Confirmação de recebimento | até **72h** |
| Avaliação inicial / triagem | até **7 dias** |
| Correção e disclosure coordenado | conforme severidade |

Pedimos um prazo razoável para correção antes de qualquer divulgação pública.

## 🛡️ Boas práticas no código

- Autenticação via **OAuth 2.0 / JWT RS256** — nunca exponha a private key; valide
  sempre pela public key.
- O `Agro-Core` (IdP) só fala com os back-ends por `/internal/*`; clientes nunca
  acessam o IdP diretamente.
- **Nunca** commite segredos (`.env`, chaves, tokens). Use variáveis de ambiente.
- Valide entradas com **class-validator** nos DTOs.

## 🎯 Escopo

Em escopo: os serviços de produção do ecossistema Leite Fácil (web, mobile, BFF,
Agro-Core, ADM, coleiras IoT).
Fora de escopo: ambientes locais/de teste e dependências de terceiros (reporte ao
mantenedor upstream).
