<div align="center">

<h1>Questly</h1>

<p><strong>Plataforma SaaS de geração e correção automatizada de provas</strong></p>

<p>
  <a href="#"><img src="https://img.shields.io/badge/.NET-10-512BD4?style=flat-square&logo=dotnet" alt=".NET 10"/></a>
  <a href="#"><img src="https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL"/></a>
  <a href="#"><img src="https://img.shields.io/badge/licenca-Proprietaria-dc2626?style=flat-square" alt="Licenca Proprietaria"/></a>
  <a href="#"><img src="https://img.shields.io/badge/status-em%20desenvolvimento-f59e0b?style=flat-square" alt="Status"/></a>
</p>

</div>

---

## Visao Geral

Questly e uma plataforma SaaS que permite professores **criar, gerar e corrigir provas automaticamente** — iniciando como uma ferramenta de avaliacao focada e evoluindo para um sistema completo de gestao escolar.

Professores constroem um banco de questoes, geram versoes randomizadas por aluno a partir de uma unica configuracao e exportam PDFs prontos para impressao em lote. Versoes futuras incluirao correcao via OCR com QR Code, assistencia de IA e billing institucional.

## Funcionalidades

- **Banco de Questoes** — crie e gerencie questoes organizadas por materia, topico e dificuldade
- **Provas Randomizadas** — gere versoes unicas por aluno com seed deterministico
- **Exportacao de PDF em Lote** — PDFs prontos para impressao gerados via QuestPDF
- **Controle de Acesso por Perfil** — perfis de Professor e Instituicao com autenticacao JWT
- **Gestao Institucional** — instituicoes gerenciam multiplos professores e turmas
- _(Planejado)_ **Correcao via OCR** — escaneie e corrija provas automaticamente via QR Code
- _(Planejado)_ **Assistencia de IA** — geracao de questoes e calibracao de dificuldade

## Stack Tecnologica

| Camada         | Tecnologia            |
| -------------- | --------------------- |
| API            | .NET 10 Web API       |
| Banco de Dados | PostgreSQL            |
| ORM            | Entity Framework Core |
| Geracao de PDF | QuestPDF              |
| Autenticacao   | JWT Bearer            |

## Arquitetura

Questly e construido como um **monolito modular** projetado para evolucao futura em microsservicos.

```
src/
├── Questly.API/              # Ponto de entrada — controllers, middlewares, DI
├── Questly.Application/      # Casos de uso, handlers CQRS, DTOs
├── Questly.Domain/           # Entidades, objetos de valor, logica de dominio
├── Questly.Infrastructure/   # EF Core, repositorios, servicos externos
└── Questly.Shared/           # Recursos transversais, tipos de resultado
```

**Modulos:**

- `Identity` — usuarios, instituicoes, autenticacao
- `Academic` — materias, topicos, banco de questoes
- `Assessment` — criacao de provas, versionamento, atribuicao a alunos
- `Generation` — motor de randomizacao, exportacao de PDF
- _(Planejado)_ `Correction` — escaneamento via OCR e QR Code
- _(Planejado)_ `Billing` — gestao de assinaturas e uso

## Fluxo de Geracao de Prova

```
Professor seleciona turma e topico
               ↓
Sistema busca questoes filtradas por dificuldade
               ↓
Randomizacao com seed deterministico (reproduzivel por aluno)
               ↓
ExameVersao individual gerado por aluno
               ↓
Exportacao de PDFs em lote
```

## Como Executar

> Pre-requisitos: [.NET 10 SDK](https://dotnet.microsoft.com/download), [PostgreSQL 16+](https://www.postgresql.org/download/), [Docker](https://www.docker.com/) _(opcional)_

```bash
# Clone o repositorio
git clone https://github.com/seu-usuario/questly.git
cd questly

# Configure a conexao com o banco
cp appsettings.Example.json appsettings.Development.json
# Edite appsettings.Development.json com suas credenciais do PostgreSQL

# Aplique as migrations
dotnet ef database update --project src/Questly.Infrastructure

# Execute a API
dotnet run --project src/Questly.API
```

A API estara disponivel em `https://localhost:5001`. Swagger UI em `https://localhost:5001/swagger`.

## Roadmap

| Fase                  | Escopo                                                       | Status          |
| --------------------- | ------------------------------------------------------------ | --------------- |
| 1 — CRUD Base         | Auth, Instituicoes, Professores, Materias, Topicos, Questoes | 🔨 Em andamento |
| 2 — Geracao de Provas | Motor de randomizacao, ExameVersao por aluno                 | ⏳ Planejado    |
| 3 — Exportacao de PDF | Templates QuestPDF, geracao em lote                          | ⏳ Planejado    |
| 4 — Turmas e Alunos   | Gestao de turmas, atribuicao de alunos, distribuicao         | ⏳ Planejado    |
| 5 — Refinamentos      | Banco publico de questoes, performance, melhorias gerais     | ⏳ Planejado    |

## Contribuicao

O projeto esta em desenvolvimento inicial e ainda nao esta aberto para contribuicoes externas.

## Licenca

Este projeto e um software proprietario e confidencial. Todos os direitos reservados. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.
