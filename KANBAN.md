# Escolaris — Kanban das Sprints

Acompanhamento das sprints do projeto. Fonte dos requisitos: [`README.md`](../README.md).
Atualize este arquivo ao mover cada card (commit sugerido: `docs: atualiza kanban sprint N`).

## Legenda

| Símbolo | Significado |
|---|---|
| ⬜ | Pendente |
| 🔄 | Em desenvolvimento |
| 🔍 | Em revisão / testes |
| ✅ | Concluído |

**Prioridade:** A = MVP · M = média · B = baixa
**Pontos:** estimativa em Fibonacci (1, 2, 3, 5, 8). Ajuste conforme sua velocidade real.
**Camadas:** Design (Figma) · Back (Spring Boot) · Front (Angular) · Testes

## Quadro geral

| Sprint | Foco | Pontos | Período | Status |
|---|---|---|---|---|
| 0 | Setup do projeto | — | __/__ a __/__ | ⬜ |
| 1 | Autenticação, perfis e usuários | 15 | __/__ a __/__ | ⬜ |
| 2 | Cadastros base e matrícula | 18 | __/__ a __/__ | ⬜ |
| 3 | Grade horária e frequência | 18 | __/__ a __/__ | ⬜ |
| 4 | Notas, boletim e fechamento de período | 19 | __/__ a __/__ | ⬜ |
| 5 | Comunicação, materiais e atividades | 27 | __/__ a __/__ | ⬜ |
| 6 | Relatórios, auditoria, dashboards e deploy | 22 | __/__ a __/__ | ⬜ |

**MVP:** Sprints 0 a 4 (mais comunicados básicos, HU09 e HU26, da Sprint 5).

## Definition of Done

Um card só vai para ✅ quando:

- [ ] Critérios de aceite da história atendidos
- [ ] Regras de negócio (RN) e requisitos (RF) relacionados implementados
- [ ] Testes unitários e de integração passando no CI
- [ ] Pull request revisado e mergeado na `develop`
- [ ] API documentada no Swagger
- [ ] Tela fiel ao protótipo do Figma e responsiva

## Fluxo de trabalho

1. Escolha o próximo card da sprint e marque 🔄.
2. Crie a branch: `feature/hu13-lancar-notas`.
3. Commits no padrão: `feat(notas): valida faixa 0-10 (RN20)`.
4. Abra o PR com `Closes #issue`; marque 🔍.
5. Após o merge e a DoD cumprida, marque ✅.

---

## Sprint 0 — Setup

**Meta:** back, front e banco rodando juntos, com CI e design system base.

- [ ] Repositório com `back-end/`, `front-end/`, `docs/` e README na raiz
- [ ] Branches `main` e `develop`; proteção da `main`
- [ ] GitHub Project (kanban), milestones das sprints e labels
- [ ] Issues das 30 HUs criadas e ligadas ao projeto
- [ ] `docker-compose.yml` com PostgreSQL
- [ ] Back: dependências, `application.yml`, migration `V1`, `/actuator/health` respondendo `UP`
- [ ] Front: estrutura `core/`, `shared/`, `features/`; proxy para a API
- [ ] Front chama `/api/actuator/health` e exibe o status
- [ ] `.gitignore` revisado (target, node_modules, .angular, dist)
- [ ] CI (GitHub Actions): build e testes do back e do front
- [ ] Figma: design system base (cores, tipografia, botão, input, tabela, card)
- [ ] Figma: telas de login e dashboard (baixa fidelidade)

---

## Sprint 1 — Autenticação, perfis e usuários

**Meta:** login com JWT funcionando e controle de acesso por perfil.
**Regras:** RN01, RN03, RN04 · **Requisitos:** RF01–RF05, RNF01, RNF02

| ID | História | Prio | Pts | Design | Back | Front | Testes | Status |
|---|---|---|---|---|---|---|---|---|
| HU01 | Login | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU02 | Recuperar senha | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU03 | Editar perfil | M | 2 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU30 | Gerenciar usuários e perfis | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

**Tarefas técnicas**
- [ ] Entidades `Usuario` e `Perfil`; migration
- [ ] Spring Security + JWT + BCrypt
- [ ] Guards e interceptors no Angular
- [ ] Bloqueio após 5 tentativas falhas (RN03)

---

## Sprint 2 — Cadastros base e matrícula

**Meta:** gestão consegue cadastrar a base escolar e matricular alunos.
**Regras:** RN05–RN10, RN13, RN14, RN36 · **Requisitos:** RF06–RF16

| ID | História | Prio | Pts | Design | Back | Front | Testes | Status |
|---|---|---|---|---|---|---|---|---|
| HU19 | Cadastrar alunos | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU20 | Cadastrar professores | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU21 | Gerenciar turmas e disciplinas | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU22 | Matricular e enturmar | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

**Tarefas técnicas**
- [ ] Entidades: Aluno, Responsável, Professor, Disciplina, AnoLetivo, Período, Série, Turma, Matrícula
- [ ] Validação de CPF e unicidade (RN10)
- [ ] Geração do número de matrícula (RN07)
- [ ] Paginação, busca e filtros nas listagens (RF12)
- [ ] Exclusão lógica (RN36)

---

## Sprint 3 — Grade horária e frequência

**Meta:** grade montada sem conflitos e frequência registrada pelo professor.
**Regras:** RN11, RN12, RN15–RN19 · **Requisitos:** RF17–RF20

| ID | História | Prio | Pts | Design | Back | Front | Testes | Status |
|---|---|---|---|---|---|---|---|---|
| HU24 | Montar grade horária | A | 8 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU06 | Ver grade horária (aluno) | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU11 | Ver minhas turmas (professor) | A | 2 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU12 | Registrar frequência | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

**Tarefas técnicas**
- [ ] Entidades: Alocação, HorárioAula, Aula, Frequência
- [ ] Detecção de conflito de professor e sala (RN11, RN12)
- [ ] Cálculo do percentual de frequência (RN16)
- [ ] Restrição de data com aula na grade (RN18)

---

## Sprint 4 — Notas, boletim e fechamento de período

**Meta:** ciclo completo de avaliação: lançar notas, calcular médias e fechar o período.
**Regras:** RN20–RN29 · **Requisitos:** RF21–RF25, RF35

| ID | História | Prio | Pts | Design | Back | Front | Testes | Status |
|---|---|---|---|---|---|---|---|---|
| HU14 | Criar avaliações | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU13 | Lançar notas | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU04 | Ver boletim | A | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU05 | Ver frequência (aluno) | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU25 | Fechar e reabrir períodos | M | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

**Tarefas técnicas**
- [ ] Entidades: Avaliação, Nota
- [ ] Média ponderada, média final e recuperação (RN21–RN25)
- [ ] Situação final do aluno (RN26, RN27)
- [ ] Trava por período fechado (RN28)
- [ ] Testes unitários das regras de cálculo, com tabela de casos

---

## Sprint 5 — Comunicação, materiais e atividades

**Meta:** comunicação da escola e ciclo de atividades entre professor e aluno.
**Regras:** RN30–RN35 · **Requisitos:** RF26–RF34

| ID | História | Prio | Pts | Design | Back | Front | Testes | Status |
|---|---|---|---|---|---|---|---|---|
| HU26 | Publicar comunicados e eventos | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU09 | Ler comunicados | A | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU17 | Enviar comunicado à turma | M | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU10 | Ver calendário | M | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU15 | Publicar material | M | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU07 | Acessar materiais | M | 2 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU16 | Criar e corrigir atividades | M | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU08 | Entregar atividade | M | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

**Tarefas técnicas**
- [ ] Definir armazenamento de arquivos (disco local, S3 ou MinIO)
- [ ] Limite de tamanho e tipos de arquivo (RN33)
- [ ] Comunicado arquivado, nunca excluído (RN35)

> Sprint mais pesada (27 pontos). Se necessário, mova HU07 e HU15 para a Sprint 6.

---

## Sprint 6 — Relatórios, auditoria, dashboards e deploy

**Meta:** fechamento do produto com relatórios, rastreabilidade e implantação.
**Regras:** RN29, RN37 · **Requisitos:** RF36–RF44, RNF03–RNF12

| ID | História | Prio | Pts | Design | Back | Front | Testes | Status |
|---|---|---|---|---|---|---|---|---|
| HU23 | Transferir ou encerrar matrícula | M | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU27 | Emitir relatórios e boletins | M | 8 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU28 | Dashboard gerencial | B | 5 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU29 | Consultar auditoria | B | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| HU18 | Ver alunos em risco | B | 3 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

**Tarefas técnicas e não funcionais**
- [ ] Geração de PDF do boletim e exportação CSV/PDF dos relatórios
- [ ] `LogAuditoria` para notas, frequência e matrícula (RF44)
- [ ] Dashboards por perfil (RF41–RF43)
- [ ] Revisão de acessibilidade WCAG 2.1 AA (RNF06)
- [ ] Revisão de LGPD e dados de menores (RNF03, RN37)
- [ ] Cobertura mínima de 70% no back (RNF07)
- [ ] Logs estruturados e tratamento padrão de erros (RNF11)
- [ ] Dockerfile do back e do front; Docker Compose completo (RNF12)
- [ ] Backup do banco (RNF10)
- [ ] Deploy e README final com instruções de execução

---

## Product Backlog (fora das sprints)

| Item | Origem | Status |
|---|---|---|
| Perfil Responsável (acesso de leitura ao aluno vinculado) | Escopo, fase 2 | ⬜ |
| Notificações por e-mail | Evolução de RF32 | ⬜ |
| Modelo multi-escola | Ponto em aberto | ⬜ |

## Decisões em aberto

- [ ] Bimestres ou trimestres?
- [ ] Armazenamento de arquivos (local, S3 ou MinIO)
- [ ] Banco: PostgreSQL ou MySQL
- [ ] Perfil Responsável no MVP ou na fase 2?

## Retrospectivas

Preencha ao fim de cada sprint.

| Sprint | O que foi bem | O que melhorar | Ações |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
